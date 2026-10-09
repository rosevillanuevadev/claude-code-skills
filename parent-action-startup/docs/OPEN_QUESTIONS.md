# Open Questions

## Product
- Is the strongest initial wedge absence/excuse, inbound notice tracking, or both?
- How much manual entry will parents tolerate before extraction is necessary?
- Does a parent need a general school notice archive or only action-linked records?
- Should teacher acknowledgment be a one-click action or require identity confirmation?
- How should separated/co-parenting/guardian restrictions work?
- How should an assistant/delegate permission model work?

## Market
- Will parents pay directly for this problem at consumer SaaS pricing?
- Will schools accept parent-originated formal notices delivered through a third-party service?
- Which school segment has the least procurement friction?
- Do small independent schools have enough pain to pay for a narrow tool instead of a suite?

## Legal/privacy
- What child data can be avoided entirely?
- What legal status does a digital excuse/absence notice need in target jurisdictions?
- When does an acknowledgment become an electronic signature?
- What retention periods do schools expect?

## Technical
- final web framework
- auth provider
- DB/storage provider
- email provider
- token strategy
- extraction model/provider if added

## Commercial
- parent subscription first vs school contract first
- school pricing unit: flat / enrollment band / active families
- free tier vs trial

## Added in Phase 0 session 1 (2026-10-09)

### Product
- OQ-P1: Does V0.1 let a parent send a response back to the school for an inbound notice (reusing the send/acknowledge machinery), or only track inbound items themselves? (audit A2)
- OQ-P2: Attachments on absence notices: leave out of V0.1? A doctor's note is health data about a minor. (audit A5)
- OQ-P3: Siblings at one school, same day: one combined message or one per child? (audit B8)
- OQ-P4: Which languages must V0.1 email templates and reason categories support? (audit B9)
- OQ-P5: Do parents need an archive of notices that require no action, or only action-linked records?

### Technical
- OQ-T1: Sending identity: product domain as From with parent as Reply-To? How do we test deliverability to Google Workspace and Microsoft 365 school mail before a pilot? (audit B1)
- OQ-T2: Abuse controls for outbound email: recipient caps, report/block link, confirmation of new recipient addresses. (audit B10)
- OQ-T3: Accept ADR-0005 (stack) after the verification checklist in `docs/TECH_STACK_OPTIONS.md`.

### Legal and privacy
- OQ-L1: What does a link click actually prove, and how should the recipient page word it? (audit B2)
- OQ-L2: How do immutable sent snapshots coexist with deletion/erasure requests? (audit B4)
- OQ-L3: Database region and data-residency expectations for the first target markets.
- OQ-L4: Which reason-note and attachment practices keep health details out of the system by default?

### Market
- OQ-M1: First pilot segment and country (independent schools? a specific country's norms around diary excuses?). (audit B12)
- OQ-M2: Will schools accept a parent-originated digital record in place of the paper diary entry? This is the real gate for the absence wedge (bootstrap question 7).

### Roadmap
- OQ-R1: Approve ADR-0006 (minimal acknowledgment link in V0.1)? (audit A1)
