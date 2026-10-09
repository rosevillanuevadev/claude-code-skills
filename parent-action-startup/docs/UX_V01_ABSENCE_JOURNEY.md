# V0.1 User Journey: Parent Reports an Absence, Teacher Has No Account

Status: draft for prototype testing. Uses synthetic people: Alex Parent, child Sam, adviser at Northfield Academy.

## Target
- Returning parent, saved contact: **45 seconds or less**, about 6 taps.
- First-ever send, including adding a child and a teacher email: **3 minutes or less**. Measured separately; do not hide onboarding cost inside the one-minute claim.
- Teacher: acknowledge in **1 tap**, no signup, no app.

## Parent flow (returning user)

Entry: Home screen, big primary button "Report absence" (also reachable from a child's page).

| Step | Screen | Default / behavior | Taps |
|---|---|---|---|
| 1 | Who | Child preselected if only one; otherwise last-used child. Chips for each child. | 0 to 1 |
| 2 | When | Chips: **Today**, **Tomorrow**, **Pick dates**. Pick dates opens a range picker. Dates are calendar dates in the school's timezone. | 1 |
| 3 | Why | Chips: Illness, Appointment, Family matter, Travel, Other. Optional one-line note ("Optional, skip health details"). No attachment in V0.1 (see audit A5). | 1 |
| 4 | To | Prefilled with the child's saved school contact. Tap to change or add another recipient. | 0 |
| 5 | Review | Shows the exact message the teacher will receive, rendered as the email. Checkbox "Ask the school to confirm receipt" on by default. | 0 to 1 |
| 6 | Send | Single button. Confirmation screen: "Sent to Ms. Reyes. We'll show when she confirms." Item appears under **Waiting on school**. | 1 |

Rules:
- Steps 1 to 4 can live on one scrollable screen; review is a second screen. Two screens total.
- No account fields, no settings, no feature tour after first use.
- "Undo" for 10 seconds after Send is nice-to-have; sending is otherwise irreversible and corrections are new linked records (never edit a sent snapshot).

## First-run additions (one time only)
1. Email magic link or code to sign in (no password).
2. Add child: display name (required), class or section (optional). No date of birth.
3. Add school contact: school name, contact name, email. Optional "this is my child's adviser/teacher".
4. Continue into the flow above.

## What the teacher receives (email)

Plain, short, readable on a phone. No images required.

```
Subject: Absence notice: Sam, Mon 12 Oct 2026

Alex Parent (verified email) reports that Sam (Grade 4, Section B) will be
absent on Monday 12 October 2026.

Reason: Illness
Note: (none)

Sent via <ProductName> on 9 Oct 2026, 7:42 PM (Asia/Manila).

[ Confirm received ]   [ I need more information ]

This notice was sent by a parent. Whether the absence is excused is
determined by your school's policy.
Not expecting this? Report it: <link>
```

Design notes:
- From address is the product's sending domain; Reply-To is the parent so a direct reply still works (open item B1 in the audit).
- The wording "verified email" appears only because the parent's address was verified at signup. It does not claim the person is the guardian of record.
- Footer carries the "not excused automatically" statement (spec 003) and an abuse/report link (audit B10).

## What the teacher sees after tapping the link
- One page, one record, no login, no navigation to anything else, no unrelated family data.
- Top: the same message as the email. Below: two buttons.
  - **Confirm received**: records timestamp and the recipient email the link was sent to. Page changes to "Thanks, the parent has been told."
  - **I need more information**: short text box (500 characters), then Send. Parent is notified.
- Link expiry: default 30 days; page after expiry says "This link has expired" with no data shown.
- The page states plainly what the click means: "We will tell the parent you received this." It does not claim to verify who is clicking.

## Parent-side states for the item

| Event | Parent sees | Section |
|---|---|---|
| Sent, awaiting | "Sent to Ms. Reyes, 7:42 PM" | Waiting on school |
| Teacher confirms | "Confirmed by Ms. Reyes, Mon 8:05 AM" | Done |
| Teacher asks for info | "Ms. Reyes asked: <text>" with a Reply action | Needs your action |
| Bounce / delivery failure | "Couldn't deliver to the saved address. Fix the address and resend." | Needs your action |
| No response by absence date | Gentle reminder to the parent (not to the teacher): "Still unconfirmed. Resend or contact school another way." | Waiting on school |

Nothing auto-nags the teacher. Reminders to school recipients belong to the later workspace phase.

## Edge cases to test in the prototype
1. **Correction:** parent chose the wrong date. Sends a new notice marked "Correction" linked to the original; the original stays visible and unchanged.
2. **After-the-fact excuse:** child already returned. "When" accepts past dates; wording shifts to "was absent". May be sent as a separate excuse letter (spec 003).
3. **Siblings, same school, same day:** two sends vs. one combined message (audit B8). Prototype both and watch the teacher's reaction.
4. **Two recipients** (class teacher + office): one record, two links; parent sees each confirmation separately.
5. **The diary problem:** the school may still require the paper diary entry. The product cannot change that. The prototype must test whether schools accept the digital record as the formal one, which is the real gate (bootstrap question 7). Consider a neutral "Download a copy" for the parent only if interviews show it matters; otherwise out of scope.
6. **Spam filter:** message lands in junk. Test with at least two real school-style mail systems (Google Workspace, Microsoft 365) using synthetic content before any pilot.

## Metrics for this prototype test
- Time to send (returning and first-run) and number of taps.
- Teacher time to confirm and where they hesitate.
- Percentage of teachers who confirm vs. ignore.
- Whether teachers say they would accept this in place of a diary entry. Qualitative, recorded in `research/EVIDENCE_LOG.md` as interview evidence.

## Out of scope for this flow
Attachments (pending OQ-P2), delegation (Phase 2), notice extraction, calendar, chat, school workspace.
