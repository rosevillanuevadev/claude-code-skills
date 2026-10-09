# Information Architecture: Parent Experience (Low Fidelity)

Principle: open, see what needs attention, act, leave. Three destinations at most.

## Sitemap

```
Home (Actions)
 ├─ Needs your action   (default segment)
 ├─ Waiting on school
 └─ Done
     └─ Item detail  (original source, history, next step)
New  (a bottom sheet, not a page)
 ├─ Report absence      -> absence flow (2 screens)
 ├─ Add school notice   -> manual action entry (Phase 1)
 └─ Send excuse letter  -> same flow as absence, different wording (spec 003)
Family
 ├─ Children   (name, optional class/section, school)
 ├─ Schools & contacts   (school name, contact name, email)
 └─ [Phase 2] Helpers   (spouse, assistant, caregiver)
Account  (reached from Family; email, timezone, language, export, delete)
```

Navigation: bottom bar with **Actions**, **+ (New)**, **Family**. Account lives inside Family. No dashboard, no feed, no calendar, no analytics.

## Home wireframe

```
┌──────────────────────────────┐
│ Today                 [Sam][Mia]│   child filter chips (All by default)
│                              │
│ [ Needs action 2 ][ Waiting 1 ][ Done ]   segmented control
│                              │
│ ┌──────────────────────────┐ │
│ │ Mia  Museum Trip Consent │ │
│ │ Sign and return by 20 Oct│ │   action stated in plain words
│ │ You · Manual entry   ›   │ │   next actor + source badge
│ └──────────────────────────┘ │
│ ┌──────────────────────────┐ │
│ │ Sam  Ms. Reyes asked a   │ │
│ │ question about 12 Oct    │ │
│ │ You · Absence notice  ›  │ │
│ └──────────────────────────┘ │
│                              │
│ [ Actions ]   ( + )  [ Family ]│
└──────────────────────────────┘
```

Row anatomy (from spec 001): child, concise title, required action, due date if any, next actor, source indicator. A row is tappable; nothing else is needed on the list.

Empty state for Needs action: "You're all set." with the **Report absence** button below. This is the only promotional element and it is a task, not an ad.

## Item detail wireframe

```
┌──────────────────────────────┐
│ ‹ Back                       │
│ Sam · Absence notice         │
│ Mon 12 Oct 2026 · Illness    │
│                              │
│ Status: Waiting on school    │
│ Sent to Ms. Reyes  Fri 7:42 PM│
│ Confirmed: not yet           │
│                              │
│ [ View what was sent ]       │   immutable snapshot (original source)
│ [ Resend ]  [ Send correction ]│
│                              │
│ History                      │
│  Fri 7:42 PM  Sent           │
│  Fri 7:42 PM  Delivered      │
└──────────────────────────────┘
```

For a school-to-parent item the "View what was sent" slot becomes **View original** (photo/PDF/text, Phase 3 preserves uploads). Spec 001: original reachable in one tap.

## State model shown to the parent

Single derived label per item (audit A3):

| Label | Condition |
|---|---|
| Needs your action | owner is parent or delegate, not completed |
| Waiting on school | owner is school, not completed |
| Done | completed or cancelled |

No "read but maybe needs action" state (spec 001). Notices that require nothing are not shown as actions at all; if the parent wants an archive, that is a separate decision (OQ-P5).

## Child and school setup screens (minimal)
- Child: name, class/section optional, school (pick or add). Nothing else.
- School: name, timezone (auto from device, editable, because absence dates are in school-local time), contacts list.
- Contact: name, role (free text), email. Phone optional and probably unused in V0.1.

## Deliberately absent
Settings page with toggles, notification center, calendar view, search (not needed under about 100 items), message threads, profile pictures, onboarding tour, ratings, social or sharing.

## Open IA questions
- Should "Done" auto-collapse after 30 days or stay as per-child history (spec: history per child)?
- Does a returning parent want a persistent shortcut to "Report absence" on Home when Needs action is non-empty? Test both placements.
- Child filter chips vs. grouping by child: chips are assumed; verify with 2-child households.
