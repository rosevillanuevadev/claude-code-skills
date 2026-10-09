# Spec 004 — Notice Ingestion Assistance

Deferred until the parent-only action model works.

## Goal
Reduce the work of turning a school notice into an actionable record.

## Inputs
- paste text
- upload screenshot/image
- upload PDF
- forwarded email later

## Suggested extraction
- child
- school
- title
- event/action date
- due date
- required parent action
- amount to bring/pay only if present in source
- items to bring
- source contact

## Safety/product rule
Never silently convert extraction into authoritative data.

Show:
- extracted suggestion
- link/view of original source
- confidence/uncertainty only if useful
- parent confirmation before saving critical fields

No generic chatbot is required.
