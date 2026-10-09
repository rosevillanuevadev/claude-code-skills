# Competitor Research Plan (Phase 0)

Date: 2026-10-09. Status: **plan only**. No external claims have been verified yet; everything below about competitors is a hypothesis from the seed docs and must be checked before it enters `EVIDENCE_LOG.md`.

## Method (applies to every competitor)
- One file per competitor in `research/competitors/<name>.md`, using the template at the bottom.
- Every claim gets: source URL, access date, type (verified fact / vendor claim / user review / inference / hypothesis). Marketing pages never count as evidence of adoption or satisfaction (AGENTS.md section 9).
- Behavior beats feature lists. Where a free trial or demo exists, walk the absence/excuse and consent flows and record step counts and time.
- Use the Wayback Machine for historical pricing and early product pages (needed for Parentapps).
- Review mining: sample 1 to 3 star reviews, tag by theme (onboarding, notification overload, reliability, complexity, integrations, support), count tags, record sample size and date range.
- Filings and press: Companies House (UK), press releases, acquirer announcements. Financial terms only if publicly disclosed; otherwise "not disclosed".

## Selection: Parentapps + the 5 closest

Selection test: closeness to the *wedge* (parent-originated formal actions, no-account recipient, lightweight), not closeness by feature count.

| Rank | Competitor | Why it is on the short list | Key question it answers |
|---|---|---|---|
| 0 | **Parentapps Connect** | Origin story matches ours; historical case study | How did a narrow parent-letter product reach hundreds of schools, and what changed after acquisition? |
| 1 | **consent.app** | Narrow consent/forms collection; closest to "one job" | Can a parent or school use it without a heavy suite? Is the recipient flow account-free? |
| 2 | **Permission Click (PowerSchool)** | Consent/permission-slip workflow owned by a large vendor | What does the incumbent flow cost, require, and omit? What did it become after acquisition? |
| 3 | **Operoo** | Forms, consent, parent-held data; school-bought | How does a parent-held record model work, and where does the complexity come from? |
| 4 | **ParentSquare** | Suite benchmark with absence reporting in many deployments (verify) | What do parents complain about at suite scale? Is absence reporting no-account for staff? |
| 5 | **One parent-first tool, chosen after triage** | We are parent-first; most of the matrix is school-first | Is anyone already doing parent-side action tracking, and does it survive? |

Parent-first triage (half a day, before deep work): quickly check Plancove, CoFamy, School Flow, Friday Folder, Sense, ParentFlow, FamilyHero, SchoolParent.ai, Schoolee for (a) still operating, (b) parent can onboard without a school, (c) handles outbound formal actions, (d) any traction evidence. Pick the single closest as slot 5. Default if triage is inconclusive: Plancove (named first in the seed matrix; unverified).

Not in the 5 but not dropped:
- **Tier 2, regional/likely-local (verify geography first):** ParentCom, Crayon Post, edjufy, Schoolinked, Eunika Academe, JARASNA. Given the team context (Philippines is one candidate first market, though the product is global), these may be the true local competitors and deserve a fast pass after the core 6.
- **Tier 3, suites for baseline only:** Bloomz, ClassDojo, Remind, School Stream, FinalForms, ParentSignature. One-page profile each; no deep dive.
- **Case study track:** SmartPass (see `SMARTPASS_CASE_STUDY.md`), run in parallel since it is mostly public-record work.

## Priority order and effort

| Order | Work | Effort | Output |
|---|---|---|---|
| 1 | Parent-first triage (9 tools) | 0.5 day | One-page shortlist table; pick slot 5 |
| 2 | Parentapps forensic case study | 1.5 days | Fills every section of `PARENTAPPS_CASE_STUDY.md` |
| 3 | consent.app + Permission Click + Operoo walkthroughs | 2 days | Three competitor files with behavior notes and screenshots stored in `local_data/` (not committed if they contain any real data) |
| 4 | ParentSquare + slot-5 profile | 1 day | Two competitor files |
| 5 | Review mining across all six | 1 day | Theme counts per competitor |
| 6 | Cross-cut synthesis against the 10 analysis questions | 0.5 day | Section in `COMPETITOR_MATRIX.md`: gaps and kill/modify signals |
| 7 | SmartPass case study | 0.5 day | Fill `SMARTPASS_CASE_STUDY.md` |
| 8 | Tier 2 regional pass | 1 day | Short profiles |

Rough total: 8 working days of research effort. Items 2 and 3 are the highest value; if time is short, do triage, Parentapps, and consent.app first.

## Parentapps: specific investigation checklist
Re-verify every "starting fact" in `PARENTAPPS_CASE_STUDY.md` (founding year, founders, investors, 2021 acquisition by Community Brands UK, 1,000+ schools claim, historical pricing). Treat each as a hypothesis until sourced. Then answer the document's own sections: founding, go-to-market, product evolution (launch features vs. later payments, bookings, MIS integrations), economics, acquisition, and the split between lessons that still hold and lessons that depended on 2015.

Specific output wanted: a timeline of product scope vs. date, so we can see whether a narrow letter product expanded into a suite and *why* (customer demand vs. growth pressure). That is the main input to our scope-discipline decision.

## What would change our mind
Mapped to the kill/modify signals in `VALIDATION_PLAN.md`:
- A competitor already offers parent-initiated absence/excuse with a no-account recipient at low price, with good reviews.
- Review mining shows parents' pain is *not* fragmentation but something we do not address (for example, schools simply refuse third-party senders).
- Parent-first tools exist and are dead: a signal about willingness to pay, not necessarily about the idea.

## Competitor file template

```
# <Name>
Accessed: YYYY-MM-DD
Profile: HQ, founded, founders, funding, ownership (each line tagged fact/claim/inference with URL)
Who buys / who uses / school adoption required? / parent app required?
Onboarding: steps and time observed
No-account flows: parent, teacher/recipient
Absence/excuse: steps observed, who initiates, acknowledgment
Consent/forms: steps observed
Multi-child, delegation, original source preserved, action/status model
Pricing and setup fees (with date)
Customer counts (source, date, vendor claim vs verified)
Reviews: store, rating, count, date range, theme tallies, 3 representative quotes (short)
Scope history: narrow -> suite? timeline
Our read: threat level, gap, what to copy, what to avoid (labeled inference)
```
