# V0.1 Tech Stack Options

Date: 2026-10-09. Nothing installed. Product-specific claims below (limits, pricing, platform behavior) are from general knowledge and **must be verified against current vendor docs before ADR-0005 is accepted**.

## What the stack must do in V0.1 (and nothing more)
- Magic-link or OTP sign-in for parents
- Family, child, school, contact data with strict per-family isolation
- Send transactional email with a replaceable provider
- Public, unauthenticated, per-record recipient pages guarded by an opaque token
- Immutable sent snapshots and an audit trail
- Scheduled jobs (reminders to parents, link expiry)
- Installable PWA; email is the reliable notification channel
- Export and delete for a family

Not needed yet: file uploads (see audit A5), AI, realtime, multi-tenant school workspaces, native apps.

## Option A: Next.js (TypeScript) + Supabase (Postgres, Auth) + transactional email

- **Shape:** Next.js app on a managed host; Supabase for Postgres and parent auth; Postmark or Resend behind a small `EmailSender` interface; cron for jobs.
- **Strengths:** fastest path to working auth, database, and row-level isolation; TypeScript end to end; large hiring pool; managed backups; easy to add Storage later for attachments.
- **Weaknesses:** row-level security policies for family members and later delegates are subtle and easy to get wrong; the recipient-link flow must bypass RLS through a server-side path, so there are two security models to keep correct; platform coupling creeps in if business logic moves into database functions or edge functions.
- **Mitigations:** keep business rules in plain TypeScript modules; use Supabase as "Postgres + Auth + Storage" only; test permissions with automated cross-family tests; store recipient tokens hashed, never in plain text; pick the database region deliberately (open question OQ-L3).
- **Ops burden:** low.

## Option B: Assembled stack (SvelteKit or Remix style framework + Neon/managed Postgres + Better Auth or similar + S3-compatible storage + Postmark)

- **Shape:** same app, but each concern is a separate vendor chosen for portability.
- **Strengths:** least lock-in; each piece replaceable; authorization lives in application code you fully control, which is simpler to reason about for the token flow.
- **Weaknesses:** more integration work up front; you own more security-sensitive glue (sessions, email verification, rate limiting); fewer batteries for a small team.
- **Ops burden:** low to medium.

## Option C: Boring monolith (Rails or Django + Postgres + Postmark, on a PaaS)

- **Shape:** server-rendered app, sprinkles of JS, installable via manifest and a small service worker.
- **Strengths:** best-in-class built-ins for forms, auth, mailers, background jobs, migrations, and admin; very good fit for a small team with one workflow; easy to keep authorization in one place.
- **Weaknesses:** diverges from the TypeScript direction in the bootstrap prompt (a preference, not a rule); less natural if a richer client-side PWA experience (offline drafts) becomes important; hiring depends on stack choice.
- **Ops burden:** low.

## Comparison

| Criterion | A: Next + Supabase | B: Assembled | C: Rails/Django |
|---|---|---|---|
| Time to working V0.1 | Fast | Medium | Fast |
| Lock-in risk | Medium | Low | Low |
| Isolation correctness effort | Medium (RLS) | Medium (app code) | Low to medium (app code) |
| Fit with TS direction | Yes | Yes | No |
| Mobile PWA polish | Strong | Strong | Adequate |
| Small-team maintenance | Good | Fair | Very good |
| Cost at pilot scale | Low | Low | Low |

## Recommendation: Option A, with guardrails

Reasons: fastest route to a demo that can go in front of parents and teachers, matches the stated TypeScript direction, and leaves a clean path to attachments and, much later, school workspaces. The honest tradeoff is that Option C would likely be at least as good for this specific workflow; I would switch to C if the team has strong Rails/Django experience or if the RLS test burden proves heavy after the first spike.

Guardrails that keep A from becoming a trap:
1. Domain logic in plain TypeScript, not in SQL functions or edge functions.
2. Provider interfaces for email (and, later, extraction); no vendor SDK calls scattered through the code.
3. Recipient tokens: random, at least 128 bits, stored as a hash, one record only, expiring, revocable; recipient pages served from server routes with no Supabase session.
4. Cross-family isolation tests run in CI from the first migration.
5. Derive the parent-facing state in one function (audit A3).
6. Rate limits and per-sender recipient caps from the first deploy (audit B10).
7. Decision checkpoint after the first vertical slice (absence send plus acknowledge page): confirm A or switch to C.

## Things to verify before accepting the ADR
- Current Supabase free/pro limits, available regions, and backup/PITR terms.
- Whether the chosen email provider allows this use (parent-originated mail to school addresses) and its deliverability tooling (dedicated sending domain, SPF/DKIM/DMARC).
- Magic-link behavior with corporate/school mail scanners that pre-click links (a known cause of consumed one-time links; prefer short codes or links that require a confirm tap).
- iOS and Android installable-PWA push behavior today.
- Any data-residency or minors'-data constraints for the first target markets (legal backlog item).

## Not decided here
Hosting vendor for the web app, analytics tooling (must exclude engagement-time metrics), error monitoring, CI provider. Decide in the first implementation session, record in the ADR.
