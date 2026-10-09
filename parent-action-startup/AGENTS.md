# AGENTS.md — Canonical Agent Instructions

This file is the primary operating contract for Claude Code, Codex, and any future coding/research agent working in this repository.

## 1. Project purpose

Build a very lightweight global parent–school action app for busy parents and independent schools.

The product should reduce the mental and administrative overhead of school notices, parent responses, absence reporting, excuse letters, and follow-up.

The company is intentionally **not** trying to build a complete school platform.

## 2. Core strategic decision

The product is **parent-first and school-compatible**.

A parent should be able to get value without requiring the school to sign a contract, migrate systems, or integrate an SIS/LMS.

School participation should improve the workflow progressively:

1. Parent-only use.
2. Teacher/school recipient can acknowledge a secure link without creating an account.
3. School can later claim/create a workspace for bulk notices, tracking, and parent action collection.

Do not invert this and make school onboarding a prerequisite for the parent MVP unless a documented ADR changes the strategy.

## 3. Product boundaries

Do not casually add:
- grades
- assignments
- report cards
- tuition/payment processing
- attendance taking
- enrollment
- classroom chat
- school social feed
- behavior/PBIS
- student analytics
- transport/dismissal
- full calendar platform
- LMS functionality
- SIS replacement
- broad family organizer features

A feature belongs only if it directly helps a parent or school **send, understand, complete, verify, or track a formal school-related action**.

## 4. Simplicity requirement

The product should feel smaller than its competitors.

Avoid building features because competitors have them. Prefer a narrow, high-quality workflow over completeness.

The intended experience is:

- open app
- see what needs attention
- act
- leave

Do not optimize for engagement time.

## 5. No integration dependency in early versions

V1 must not depend on Microsoft Teams, Google Classroom, SIS, LMS, or school database integrations.

Use simple inputs:
- manual entry
- upload/paste
- email forwarding later
- CSV import for school rosters later
- secure recipient links

Integrations require an explicit ADR and evidence that they materially improve adoption.

## 6. AI policy

AI is not the product.

The core workflow must remain useful without AI. AI may later be used invisibly for narrow tasks such as extracting a child, date, deadline, requested action, or required item from a notice. Every AI extraction must be reviewable by the parent before it becomes authoritative.

Do not add chatbots, AI dashboards, recommendations, or generative features without a specific validated job.

## 7. Data and privacy

Never commit real data about minors, schools, guardians, teachers, or customers to Git.

Use `data/synthetic/` for fake fixtures.
Use `local_data/` for private local experiments; it is gitignored.

Design for data minimization. Especially avoid collecting health/medical detail unless required. For absence reasons, prefer simple categories and make free-text optional.

Do not claim GDPR, FERPA, COPPA, UK GDPR, or other legal compliance unless requirements have been researched and reviewed. Record legal questions in `docs/OPEN_QUESTIONS.md`.

## 8. Working method for a months-long build

Before each substantive session:
1. Read this file.
2. Read `docs/STATUS.md`.
3. Read `docs/ROADMAP.md`.
4. Read relevant specs and recent ADRs.
5. State the smallest useful objective for the session.

During work:
- prefer vertical slices
- keep commits small and coherent
- do not refactor unrelated code
- do not add dependencies without justification
- do not prematurely abstract for imagined enterprise requirements
- write tests for core state transitions and permissions
- preserve a mobile-first, low-friction UX

After substantive work:
- update `docs/STATUS.md`
- update the relevant spec
- add an ADR when a meaningful product/architecture decision changed
- record unresolved issues in `docs/OPEN_QUESTIONS.md`

## 9. Research discipline

Competitor and market research must be forensic, not promotional.

For each claim, record:
- source URL
- accessed date
- exact claim or observed behavior
- whether it is fact, marketing claim, inference, or hypothesis

Never treat a competitor marketing page as proof of adoption, revenue, or customer satisfaction.

## 10. Decision hierarchy

When uncertain, prioritize in this order:
1. Does it solve the parent’s real workflow?
2. Can a parent use it without school procurement?
3. Does it remove steps instead of adding them?
4. Does it keep the product lightweight?
5. Is it safe and privacy-conscious?
6. Can a small team maintain it?

## 11. Current working thesis

A busy parent may already be paying with time, stress, or even another human assistant to keep track of school notices and formal responses. The product should replace the coordination overhead, not merely digitize paper.
