---
name: circumnavigation-distance
description: Measure the official shortest-swimmable-path distance for a swim circumnavigation (an island, peninsula, or any closed-loop route) from the swimmer's raw GPX files, and build the public route analysis page for it. Triggers on requests like "measure this circumnavigation," "compute the distance for [swimmer]'s [island] swim," "build a route analysis page," or when handed a folder of GPX leg files for a loop swim. Do not use for shore-to-shore crossings, those have a different, simpler method (straight-line tangent between two fixed points).
---

# Circumnavigation Distance Measurement

Computes the WOWSA shortest-swimmable-path distance for a circumnavigation swim from the
swimmer's own GPS track, and builds the public route analysis page for it. Full worked case
study, with every bug this method hit and how each was found and fixed:
[swim-1033-ireland-circumnavigation](https://github.com/rose2023va/swim-1033-ireland-circumnavigation).
**Read that repository's `docs/` before running this on a new swim if this is the first use in a
session.** The two failures documented there are easy to reintroduce from first principles.

## The rule

A circumnavigation cannot be measured as a straight line between two points, start and finish are
the same coordinate. The rule instead: the fewest possible waypoints, taken from the swimmer's own
GPS track, connected by straight (great-circle) lines, such that none of those lines cross land. A
waypoint is only kept where removing it would cause the line between its neighbors to cross land.

## Two hard-won rules, non-negotiable

1. **Never trust the coastline data source without checking its actual point density in a
   geometrically complex test area first.** Natural Earth's "10m" naming refers to a map-scale
   category, not point resolution, and had only ~700m average vertex spacing in a tested inlet.
   That is not precise enough. Use OSM Land Polygons instead, fetched once (globally, ~900MB, a
   one-time cost that is never repeated) and cached locally as a small per-landmass GeoJSON slice.
   Never query a live map API (Overpass or otherwise) inside the actual calculation, live queries
   were tried and failed repeatedly on reliability grounds, not just speed.

2. **Never assume GPX leg file numbers reflect the order the swimmer actually covered the coast
   in.** On a multi-session expedition swim, sections get filled in out of order for reasons
   (tides, weather, logistics) the file naming does not capture. Reconstruct the true order by
   matching every leg's start and end point against every *other* leg's endpoints, not by
   sorting filenames. This was the largest source of error in the reference build: a
   file-number-based approach found 24 false "gaps" totaling 511.7km; the corrected method found
   9 real ones totaling 15.2km. Any "gap" list built before this check is done should be treated
   as provisional, not sent to anyone.

## Workflow

1. **Get the GPX files and confirm the landmass.** One file per swim session is expected. Ask for
   the folder path if not given.

2. **Fetch and cache the coastline data**, once per landmass, reused forever after:
   `scripts/fetch_and_cache_landmass.py` in the case study repo. Takes a name and a bounding box.
   Skip this step entirely if `.cache/osm_land_<name>.geojson` already exists from a prior run.

3. **Reconstruct the true leg order**: `scripts/reconstruct_true_chain.py`. Do this even if the
   file numbers look sequential and clean, verify, do not assume. Read the printed gap list, if
   any gap is larger than roughly 10km, treat it as a real, notable finding worth confirming with
   whoever provided the files before proceeding, not just a data quirk.

4. **Run the algorithm**: `scripts/circumnav_v5_final.py`. Confirm
   `remaining_land_crossings` is exactly 0 in the output before treating the result as valid. If
   it is not zero, do not publish or report the distance, something upstream needs attention.

5. **Sanity check visually before trusting the number.** Overlay the computed route and the
   swimmer's actual raw GPX track on a real map (Google Maps or equivalent with live tiles, not a
   flat schematic) and look for daylight between them; a computed line cutting across land while
   the real track curves around it, or a long straight "gap" line while the real track runs
   continuous, both mean something upstream is still wrong. This one check caught both major bugs
   in the reference build; a test suite did not catch either. Do not skip it just because the
   numbers look plausible.

6. **Build the route analysis page**: `scripts/build_analysis_page.py`. Requires a
   `GOOGLE_MAPS_API_KEY` in the environment and a `page_data.json` shaped as described in that
   script's docstring (built from the GPX polylines, the computed route, and the gap list).
   Distinguish two different documents, do not conflate them:
   - A **route analysis document**, sent to the swimmer and observer to account for any real
     remaining gaps. Include the full GPX track, the computed route, and the gap list plainly.
   - A **public source-of-truth page**, the eventual permanent record. Should show only the final
     adopted distance, not the internal review process, rejected methods, or gap discussion.
   Do not publish the second until the swimmer and observer have responded to the first.

7. **Deploy** as a Cloudflare Worker with static assets (`wrangler deploy`). If a custom route
   path 404s even though the Worker is confirmed triggered, check `not_found_handling` in the
   assets config of `wrangler.jsonc`, set it to `single-page-application`. See
   `scripts/wrangler.jsonc` in the case study repo for the working config.

## House style

No em dashes or en dashes anywhere in generated content, including the analysis page. Use commas,
periods, or restructure the sentence.

## When something looks off

Stop and look at the map before trying to explain the number away. Every real bug in the
reference build produced a plausible-looking figure; the visual overlay in step 5 is what caught
both of them, not a sanity check on the number itself.
