# ADR-0005: V0.1 tech stack

## Status
**Proposed.** Not accepted. Needs a human decision. Do not install frameworks until accepted.

## Context
Phase 0 requires a stack decision before implementation. Requirements and the three options (Next.js + Supabase, assembled stack, Rails/Django monolith) are compared in `docs/TECH_STACK_OPTIONS.md`.

## Proposed decision
Option A: TypeScript, Next.js, Supabase used only as Postgres + Auth (+ Storage later), transactional email behind a provider interface, PWA delivery. Also confirms ADR-0003 (PWA first) for V0.1.

## Guardrails (part of the decision)
Business logic in plain TypeScript; provider interfaces for email and later AI extraction; hashed expiring single-record recipient tokens served without a Supabase session; automated cross-family isolation tests in CI; rate limits from first deploy; a go/no-go checkpoint after the first vertical slice, with Option C as the named fallback.

## Consequences
Positive: fast demo, one language, managed infrastructure, low ops.
Negative: two security models (RLS for parents, server-side tokens for recipients); some platform coupling; must verify vendor terms and region before acceptance.

## Conditions to accept
Complete the verification list in `docs/TECH_STACK_OPTIONS.md` and record results in `research/EVIDENCE_LOG.md`.
