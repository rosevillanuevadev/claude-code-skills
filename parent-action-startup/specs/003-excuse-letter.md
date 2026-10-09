# Spec 003 — Excuse Letter

## Goal
Replace the delayed paper-diary excuse workflow with a formal digital parent record.

## Distinction from absence notice
An absence notice may be sent before/during the absence. An excuse letter may be the formal explanation required by school policy, sometimes after the absence.

V0.1 may combine them in one flow when the school allows it, but the data model should allow both records.

## Output
A clean, human-readable formal message containing:
- parent/guardian identity
- child
- absence date(s)
- reason category
- optional parent note
- date/time submitted
- optional attachment

## Delivery
Initially email to saved school/teacher contact.
Later, school workspace may receive it natively.

## Status
- Draft
- Sent
- Delivered (if provider confirms)
- Opened (only if reliable/appropriate)
- Acknowledged
- Needs information
- Accepted / recorded, if school chooses to respond

Do not imply the app itself makes an absence “officially excused.” School policy controls that.
