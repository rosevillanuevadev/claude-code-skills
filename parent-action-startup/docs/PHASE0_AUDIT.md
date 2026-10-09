# Phase 0 Audit: Contradictions and Missing Decisions

Date: 2026-10-09. Scope: every file in `docs/`, `specs/`, `decisions/`, `research/`, `data/synthetic/`, plus `AGENTS.md` and the bootstrap prompt.

Synthetic data check: all four fixtures use invented names and `example.invalid` addresses. No real personal data found.

Severity: **A** = blocks V0.1 design, **B** = decide before building, **C** = note and carry.

## Contradictions

### A1. Phase 1 creates "Waiting on School" items that cannot ever resolve
- `specs/002` step 7 moves a sent absence to *Waiting on School*.
- `specs/003` defines `Acknowledged` and `Needs information` statuses.
- `specs/005` (the secure acknowledgment link) and `ROADMAP.md` place the link in **Phase 2**.
- Result: in Phase 1 every sent absence sits in Waiting forever unless the parent manually closes it. That undermines the core promise ("who needs to act next?") and makes bootstrap questions 2 and 3 untestable.
- Proposed resolution: pull the minimal link (Acknowledge, Request more info) into V0.1 and leave delegation in Phase 2. See ADR-0006 (Proposed). Roadmap not changed pending your decision.

### A2. "Waiting on School" has no meaning for school-to-parent items when the school has no workspace
- `specs/001` shows all three states for all items. For a manual "Museum Trip Consent" the parent completes the form on paper or somewhere else, so there is no school-side actor in the system.
- Today a school-to-parent item can only go Needs action -> Done (self-attested). That is fine, but it must be stated, and the UI must not imply the school was informed.
- Missing decision: does V0.1 offer a "send my response back" path for inbound items (reusing the absence/excuse email + link machinery), or is V0.1 strictly absence/excuse for outbound plus self-tracked inbound? Open question OQ-P1.

### A3. Status model is stored twice
- `DATA_MODEL.md` Action has both `owner_type` (parent / delegate / school / none) and `status` (needs_action / waiting / done / cancelled).
- These overlap: `waiting` should equal "owner is school and not done". Two sources of truth will drift.
- Proposed: store `owner_type` plus `completed_at` / `cancelled_at`; derive the parent-facing label (Needs your action / Waiting on school / Done) in one function. Add to data model review.

### A4. Open tracking vs. privacy
- `DATA_MODEL.md` Delivery has `opened_at`; `METRICS.md` tracks "recipient open rate".
- `specs/003` says "Opened (only if reliable/appropriate)". Pixel-based opens are unreliable (mail clients prefetch images) and are tracking of a school employee in a product about minors.
- Proposed: do not use tracking pixels. Treat a click on the secure link as the only "opened" signal, and label it as such. Drop open-rate from metrics; keep acknowledgment rate.

### A5. "No medical detail" vs. optional attachment
- `PRIVACY_SECURITY.md` and `specs/002` avoid medical detail, yet `specs/002` allows an optional attachment, and the most common attachment for an illness absence is a doctor's note.
- The note field and attachment are therefore a back door for health data about a minor.
- Proposed: V0.1 ships without attachments on absence (or with a plain warning and a short retention cap). Decide explicitly. Open question OQ-P2.

## Missing decisions

| # | Gap | Why it matters | Where recorded |
|---|---|---|---|
| B1 | Email sender identity: what is the From address, and how is Reply-To handled? | Cannot spoof the parent's address (SPF/DKIM/DMARC). A From of `app domain` + Reply-To parent is the usual answer, but school spam filters may quarantine it, which breaks the wedge. | OQ-T1; stack doc |
| B2 | What a recipient link actually proves | Possession of the emailed link, not the teacher's identity. Links get forwarded. Spec 005 says to document this; nothing has. | OQ-L1 |
| B3 | Trust model for schools: how does a teacher know the "parent" is a real parent? | Anyone can email a fake excuse. The diary signature was weak too, but schools will ask. Minimum: verified parent email shown on the message, plus "sent via app on <date>". | UX journey |
| B4 | Immutable sent snapshot vs. deletion/export | A legal erasure request and an immutable audit trail pull in opposite directions. Need a rule (e.g., snapshots are deletable by the family; audit metadata is minimized and retained shorter). | OQ-L2 |
| B5 | Delegate sending on behalf of a parent | `Record.created_by` alone cannot express "assistant sent on behalf of guardian". A formal excuse needs `sent_by` and `on_behalf_of`. Cheap to add now, expensive after data exists. | Data model review |
| B6 | Child identification in the message | Minimization says store little; the teacher needs enough to know which child (name, class/section). Parent-entered display name plus optional class. No DOB. | UX journey |
| B7 | Absence dates and time zones | Absence dates should be calendar dates in the **school's** timezone, not instants. Fixtures already span Asia/Manila and Europe/London, which is a good test. | Data model review |
| B8 | Sibling at the same school absent the same day | One message listing two children or two messages? Affects teacher inbox noise and the data model (one record or two). | OQ-P3 |
| B9 | Localization | Global scope, but nothing on email template language, reason-category translation, or locale-specific date format. Account has `locale`; templates do not. | OQ-P4 |
| B10 | Abuse and rate limiting | An outbound-email product with free text can be used for spam or harassment. Needs recipient confirmation rules, rate limits, and a report/block link in every message. Listed as pre-pilot; should be designed in from V0.1. | Stack doc; OQ-T2 |
| B11 | Co-parenting and restricted guardians | Listed as open; affects the permission model from day one even if unbuilt. At minimum, do not make "family owner" imply "sole authority". | Existing OQ |
| B12 | Target segment | `AGENTS.md` says "busy parents and independent schools"; nothing else narrows the market. The ADRs say global. First pilot segment decides language, policy norms, and email culture. | OQ-M1 |

## Consistency notes (no action needed)
- Bootstrap sequence (7 items) maps one-to-one to Roadmap Phases 0 to 6. Fine.
- ADR-0003 (PWA first) is still "Proposed" while AGENTS.md treats it as settled. Confirm or accept it in ADR-0005 below.
- `specs/003` correctly says the app must not claim an absence is "officially excused". Keep that language in every UI string.
- `docs/PRIVACY_SECURITY.md` correctly avoids compliance claims. Keep it that way.
- Evidence format is unspecified ("table or one file per competitor"). Decided in `research/RESEARCH_PLAN.md`: one file per competitor.
- iOS web push depends on the PWA being installed to the home screen (verify current behavior). Treat email as the reliable reminder channel, push as a bonus.
