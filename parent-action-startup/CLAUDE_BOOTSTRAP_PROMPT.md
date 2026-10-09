# Claude Code Bootstrap Prompt

You are the primary engineering/research agent for a months-long startup project. Treat the repository itself as the persistent project brain. Do not rely on this chat or your memory for durable project state.

## First actions

1. Read `AGENTS.md` completely.
2. Read `README.md`.
3. Read every file in `docs/`.
4. Read `research/COMPETITOR_MATRIX.md`, `research/PARENTAPPS_CASE_STUDY.md`, and `research/VALIDATION_PLAN.md`.
5. Read all current ADRs in `decisions/`.
6. Read the current specs in `specs/`.
7. Inspect `data/synthetic/` and confirm that no real personal data is present.

Then produce a concise project-state summary before making changes.

## Project objective

Build a lightweight global parent–school action application for busy parents.

The product exists because important school work is fragmented: paper letters, diaries, email, PDFs, school portals, Teams/Google Classroom, chat groups, and messages relayed through children. Parents often have to manually determine which child a notice belongs to, whether an action is required, what is due, who should handle it, and whether the school received the response.

The outbound flow is also unnecessarily manual. A parent may need to report an absence, contact a teacher, and then still write a formal excuse in a physical diary that the school only sees when the child returns.

The product should make those workflows simple.

### Parent promise

> Know what school needs from you. Get it done.

### Product model

School → Parent:
- notice
- acknowledge
- consent/respond
- submit requested document

Parent → School:
- report absence
- send excuse letter
- submit requested document
- formal response

Every active record should clearly answer:

> Who needs to do something next?

Parent-facing states should stay simple:
- Needs your action
- Waiting on school
- Done

## Strategic wedge

This is a **parent-first, school-compatible** product.

A parent should be able to use it before the school buys or integrates anything. Early parent actions can be sent to ordinary school/teacher email addresses. School recipients should eventually be able to acknowledge via a secure web link without creating an account.

If a school later adopts the product, it can gain a workspace for bulk notices, parent action tracking, reminders, and CSV roster import.

Do not make school procurement a prerequisite for the first useful product.

## Extremely important scope constraints

Do not turn this into an SIS, LMS, family organizer, messaging network, or parent portal suite.

Do not add by default:
- grades
- assignments
- report cards
- attendance-taking
- tuition/payments
- enrollment
- behavior tracking
- chat
- school social feed
- transport/dismissal
- broad calendar platform
- AI chatbot
- Teams/Google Classroom/SIS integrations

If a feature does not directly help the parent/school send, understand, complete, verify, or track a formal school-related action, it is probably out of scope.

## Product phases

Follow `docs/ROADMAP.md`. Do not collapse months of work into a giant first implementation.

The intended sequence is:
1. research/validation and UX
2. parent-only action inbox + absence/excuse sending
3. secure no-account school acknowledgment + delegation
4. notice ingestion/extraction assistance
5. school workspace
6. pilot hardening
7. commercialization

## Local folders and project memory

Use the repo as durable memory.

- documentation belongs in `docs/`
- feature specifications belong in `specs/`
- market/competitor evidence belongs in `research/`
- meaningful decisions belong in `decisions/` as ADRs
- committed test/demo data must be synthetic in `data/synthetic/`
- private local experiments can use `local_data/`, which is gitignored

Never commit real child, parent, teacher, school, or customer data.

## Forensic competitor work

Before finalizing V0.1, investigate the competitor set in `research/COMPETITOR_MATRIX.md`.

The research must answer more than “what features do they have?” For each serious competitor, determine where possible:
- who buys
- who uses
- whether school adoption is mandatory
- onboarding friction
- no-account parent/teacher flows
- absence/excuse workflow
- multi-child parent experience
- delegation support
- action/status model
- original source preservation
- pricing/setup fees
- customer counts and evidence dates
- company age, funding, acquisitions
- app-store review themes
- complaints about complexity, reliability, notification overload, onboarding, or integrations
- whether the product started narrow and later became a suite

Pay special attention to Parentapps as a historical case study and SmartPass as a strategic narrow-workflow case study.

Do not assume competitor existence invalidates the startup. The research question is whether there is a better, smaller, lower-friction wedge for 2026.

## Product questions to answer before coding heavily

1. Can a parent get meaningful value with no school account?
2. Can absence/excuse reporting be completed in under one minute?
3. Can a teacher acknowledge receipt without an account?
4. Is manual action entry tolerable for V0.1, or is upload/paste extraction required immediately?
5. Does delegation to spouse/assistant/caregiver materially differentiate the product?
6. What is the smallest data model that supports multiple children, guardians, schools, contacts, and immutable sent records?
7. What must be true before a school treats a digital excuse as acceptable?
8. What privacy data can be avoided completely?

## Technical direction

Do not install frameworks until the tech-stack decision is documented.

Evaluate a low-ops web/PWA architecture. A likely candidate is TypeScript + a modern web framework + managed PostgreSQL/Auth/Storage + transactional email. Supabase is a plausible early provider, not a permanent assumption.

Architecture should support:
- mobile-first PWA
- family/guardian/delegate permissions
- school contacts before school workspaces exist
- immutable sent snapshots
- secure tokenized recipient links
- attachment authorization
- audit events
- simple export/delete
- replaceable email provider
- replaceable AI extraction provider later

Do not build native mobile apps initially unless evidence clearly requires them.

## UX quality bar

The app should feel like a calm action inbox, not school software.

A parent should open it and see:
- what needs action
- what is waiting on school
- what is done

The absence flow should be a signature demonstration:

Child → date(s) → reason → optional note/attachment → recipient → review → send.

No unnecessary settings, dashboards, feeds, or analytics.

## Privacy rule

This system concerns minors. Data minimization is a product requirement.

Do not request sensitive information “just in case.” Do not store medical detail by default. Do not claim legal compliance without documented research.

## Research / build rhythm

This project may take months. Preserve continuity.

At the end of each substantial session:
- update `docs/STATUS.md`
- update the relevant spec
- create/update ADRs for meaningful decisions
- add unresolved questions to `docs/OPEN_QUESTIONS.md`
- add evidence to `research/EVIDENCE_LOG.md`

Do not silently change product direction.

## First assignment

Do **not** build the entire application.

Start with Phase 0:
1. Audit the current repo documents for contradictions or missing decisions.
2. Produce a prioritized research plan for Parentapps + the 5 closest competitors.
3. Draft the V0.1 user journey for a busy parent reporting an absence and sending an excuse to a teacher who has no account.
4. Draft the low-fidelity information architecture for the parent experience.
5. Propose 2–3 minimal technical stack options with tradeoffs, and recommend one.
6. Update `docs/STATUS.md` and `docs/OPEN_QUESTIONS.md` with the results.

Stop before framework installation or implementation unless explicitly instructed to proceed.
