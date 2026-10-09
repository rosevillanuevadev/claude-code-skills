# Spec 005 — Secure School Recipient Link

## Goal
Allow a teacher/school recipient to acknowledge a parent-originated record without installing an app or creating an account.

## Link properties
- opaque token
- limited to one record
- expires
- revocable
- does not reveal unrelated family information

## Recipient actions
V0.1 candidates:
- Acknowledge received
- Request more information

Later:
- Accepted / recorded
- Declined, only when policy requires it

## Identity
The system may know the recipient email used for delivery, but should not overstate identity verification. Document what the link actually proves.

## Parent feedback
After recipient action, parent sees updated status and timestamp.

## Phase 0 notes (2026-10-09)
- ADR-0006 (Proposed) moves the minimal subset (Acknowledge, Request more information) into V0.1.
- Use a click on the link as the only "opened" signal. No tracking pixels.
- Suggested defaults to validate: 30-day expiry, 500-character info request, token stored as a hash, 128 bits or more of randomness.
- Page copy must say what a click means ("we will tell the parent you received this") and must not claim to verify identity.
