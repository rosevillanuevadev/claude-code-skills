# Spec 002 — Report Absence

## Goal
A parent can formally notify a school/teacher about an absence in under one minute.

## Inputs
- child
- absence date or date range
- reason category
- optional note
- optional attachment
- recipient school contact

## Default reason categories
- illness
- appointment
- family matter
- travel
- other

Do not request medical diagnosis by default.

## Flow
1. Parent selects child.
2. Chooses date(s).
3. Selects reason category.
4. Adds optional note/attachment.
5. Reviews recipient and final message.
6. Sends.
7. App stores an immutable sent snapshot and moves item to Waiting on School when acknowledgment is requested.

## Acceptance criteria
- mobile completion in roughly one minute for a saved contact
- parent sees exactly what will be sent before sending
- no school account required for delivery
- failure/bounce state is visible

## Phase 0 notes (2026-10-09)
- Detailed flow, copy, edge cases, and targets: `docs/UX_V01_ABSENCE_JOURNEY.md`.
- Target split: returning parent 45 seconds or less; first-ever send 3 minutes or less, measured separately.
- Attachment is out of V0.1 pending OQ-P2.
- Step 7 depends on the acknowledgment link; see ADR-0006 (Proposed).
- Dates are calendar dates in the school's timezone, not instants.
