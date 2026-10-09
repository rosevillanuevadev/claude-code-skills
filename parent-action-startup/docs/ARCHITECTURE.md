# Architecture — Working Direction

No stack is final until an ADR is approved.

## Desired qualities
- web/PWA first
- mobile-first UX
- simple deployment
- managed infrastructure
- low operational overhead
- strong tenant/user isolation
- secure file handling
- auditable state transitions
- straightforward export/deletion
- replaceable email and AI providers

## Likely practical stack to evaluate
- TypeScript
- Next.js or equivalent modern web framework
- PostgreSQL
- managed auth
- object storage for attachments
- transactional email provider
- server-side jobs for reminders and delivery processing

A managed platform such as Supabase is a likely fit for early PostgreSQL/Auth/Storage, but this must be justified in an ADR rather than assumed forever.

## PWA first
Do not build native apps initially. A responsive PWA/web app should cover:
- parent inbox
- quick absence report
- secure recipient link
- school dashboard later

Native apps can be reconsidered only after usage proves a need for platform-specific capabilities.

## Domain boundaries
Keep these concerns separate:
- identity / account
- family / guardian relationships
- school contacts/workspaces
- communications/records
- action requirements
- delivery
- responses
- attachments
- audit events

Do not collapse child records into `parent_email` or similar shortcuts. A child may have multiple guardians, delegates, and school contacts.

## Email delivery
Parent-originated school actions may initially be delivered by email. The sent record must be immutable enough to show what was sent and when.

Secure recipient actions should use expiring, signed/tokenized links and should not expose unrelated family data.

## AI boundary
If/when extraction is introduced, keep an adapter boundary so model/provider can be replaced. Store the original source separately from extracted/suggested fields.
