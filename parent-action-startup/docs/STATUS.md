# Project Status

Last updated: 2026-10-09

## Current phase
Phase 0: Foundation and validation. No application code, no frameworks installed.

## Product thesis
A lightweight global parent-school action app for busy parents. Parent value should not require formal school adoption. The initial wedge is formal school-related actions, especially notices requiring follow-through and parent-initiated absence/excuse workflows.

## Draft V0.1 in one sentence (Phase 0 exit candidate)
A parent can report a child's absence to a teacher in under a minute and see when the teacher confirms receipt, with no school account on either side.

## Key decisions already made
- global market, not Philippines-only
- very lightweight product
- no fancy features for their own sake
- no integrations required in V1
- no grades, no full school management platform
- parent is a first-class customer/user, not merely a recipient
- repository is the persistent project brain
- synthetic data only in repo

## Phase 0 session log

### 2026-10-09 (session 1)
Done:
- Audited all docs, specs, ADRs, research seeds, and fixtures: `docs/PHASE0_AUDIT.md` (5 contradictions, 12 gaps; fixtures contain no real data).
- Prioritized competitor research plan (Parentapps + 5, tiers, effort, template): `research/RESEARCH_PLAN.md`.
- V0.1 absence journey with teacher-side flow and edge cases: `docs/UX_V01_ABSENCE_JOURNEY.md`.
- Low-fidelity parent IA and wireframes: `docs/INFORMATION_ARCHITECTURE.md`.
- Three stack options with a recommendation: `docs/TECH_STACK_OPTIONS.md`.
- Proposed ADRs: ADR-0005 (stack), ADR-0006 (pull the minimal acknowledgment link into V0.1).
- Added open questions OQ-P1..P5, OQ-T1..T3, OQ-L1..L3, OQ-M1.

Not done (deliberately): no external research performed, so no competitor claim is verified; no framework installed; roadmap unchanged.

## Decisions waiting on a human
1. ADR-0006: include the minimal acknowledgment link in V0.1? (Recommended: yes.)
2. ADR-0005: accept Option A for V0.1, after the verification checklist? (Recommended: yes, with the Option C fallback checkpoint.)
3. Attachments on absence notices: leave out of V0.1? (Recommended: yes.) See OQ-P2.
4. First target segment/market for pilots. See OQ-M1.

## Immediate next work
1. Parent-first triage and Parentapps forensic case study (research plan items 1 and 2).
2. consent.app, Permission Click, Operoo walkthroughs.
3. Click-through prototype of the absence flow and the teacher acknowledgment page for parent/teacher testing (no framework needed; a static prototype is enough).
4. Data model review incorporating audit items A3, B5, B7.
5. Privacy threat model (stub the sections in `docs/PRIVACY_SECURITY.md`).
6. Schedule the first 5 parent interviews using `research/INTERVIEW_GUIDE.md`.

## Open strategic question
Monetization order is not yet decided: parent-paid first, school-paid first, or hybrid. Do not hard-code the business model into architecture before validation.

## Repository placement note
This project currently lives in the `parent-action-startup/` folder of the `claude-code-skills` repository because that was the only repo available in the session. A dedicated repository is the better long-term home; history can be moved with `git subtree split`.
