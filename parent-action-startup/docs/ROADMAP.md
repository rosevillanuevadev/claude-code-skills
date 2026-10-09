# Roadmap

This is a months-long build. Do not rush all phases into one release.

## Phase 0 — Foundation and validation
Goal: make the product thesis, data model, workflows, privacy assumptions, and competitive position explicit before app code.

Deliverables:
- competitor forensic research
- 5–10 parent workflow interviews / diary studies
- 3–5 school-side interviews if accessible
- prototype of the core parent inbox and absence flow
- final V0.1 scope
- tech stack ADR
- data model review
- privacy threat model

Exit condition: we can explain exactly what V0.1 does in one sentence and can demo the main flow without explaining the rest of the school software market.

## Phase 1 — Parent-only V0.1
Goal: a parent can manage school action records independently.

Core:
- account
- family/children
- school and contact records
- manual action item creation
- Needs Action / Waiting / Done
- report absence
- create excuse letter
- send via email to an existing school/teacher contact
- immutable sent record
- history per child

Do not add AI or school workspaces yet unless required by a validated flow.

## Phase 2 — Recipient acknowledgment + delegation
Goal: close the loop without requiring school onboarding.

Core:
- secure recipient link
- open/acknowledge/request-more-info states
- parent sees recipient status
- parent can add spouse/guardian/assistant as delegate
- assign an action to another caregiver/delegate
- audit trail

## Phase 3 — Notice ingestion assistance
Goal: reduce manual parent entry.

Core:
- paste text
- upload image/PDF
- optional email forwarding address
- extraction suggestions: child, school, due date, action, requested item
- parent confirmation before save
- preserve original source

AI should be narrow, reviewable, and replaceable.

## Phase 4 — School workspace V0.1
Goal: a school can use the product intentionally without integrations.

Core:
- school workspace
- roles
- CSV import of students/guardians
- create structured notice
- action type: Read / Acknowledge / Respond / Submit
- select recipients
- due date
- completion dashboard
- outstanding filter
- reminder to incomplete recipients
- parent responses and submissions

## Phase 5 — Pilot hardening
Goal: run with real pilot users safely.

Core:
- security review
- data export/deletion
- rate limits
- bounce handling
- audit logs
- backup/restore plan
- onboarding
- support tools
- school-year rollover strategy
- operational monitoring

## Phase 6 — Commercialization
Goal: prove someone repeatedly pays.

Core:
- pricing experiment
- self-serve parent subscription and/or school annual plan
- billing
- terms/privacy
- support workflow
- product analytics focused on task completion, not engagement time

## Explicitly deferred
- SIS/LMS integrations
- native iOS/Android apps
- payments
- grades
- attendance-taking
- broad messaging/chat
- AI assistant/chatbot
