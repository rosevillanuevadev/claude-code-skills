# ADR-0006: Include the minimal recipient acknowledgment link in V0.1

## Status
**Proposed.** Changes the current roadmap, so it needs an explicit human decision. `docs/ROADMAP.md` is unchanged until then.

## Context
`docs/PHASE0_AUDIT.md` item A1: Phase 1 sends absence notices and moves them to "Waiting on School", but the mechanism that resolves that state (secure acknowledgment link, spec 005) is scheduled for Phase 2. Without it, every sent item stays in Waiting until the parent manually closes it, and the central claim ("who needs to act next?") is not demonstrated. Bootstrap questions 2 and 3 (one-minute absence, no-account teacher acknowledgment) also cannot be tested.

## Proposed decision
Move only these pieces of spec 005 into V0.1:
- opaque, expiring, single-record link
- two actions: Confirm received, Request more information (short text)
- parent-side status updates

Keep in Phase 2: delegation, revocation UI, accepted/declined states, multiple-recipient refinements, any school-side dashboard.

## Alternatives considered
1. Keep roadmap as is and let the parent mark "school confirmed" manually. Cheapest, but tests nothing about the wedge and trains the parent to distrust the status.
2. Remove "Waiting on school" from V0.1 for sent items (they go straight to Done). Honest, but loses the signature loop and the product-led school-adoption hypothesis.

## Consequences
Adds roughly one vertical slice to V0.1 (token model, public page, one email template, status transitions). Brings the security design for recipient links forward, which is good to learn early. Raises the importance of email deliverability testing (audit B1).
