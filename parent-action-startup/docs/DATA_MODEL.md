# Data Model — Conceptual

This is a domain model, not final SQL.

## Account
- id
- email
- display_name
- timezone
- locale
- created_at

## Family
- id
- owner_account_id
- name

## FamilyMember / Delegate
- id
- family_id
- account_id or invited_email
- role: guardian / spouse / assistant / caregiver
- permissions

## Child
- id
- family_id
- display_name
- school_id nullable
- grade_or_year optional
- section_or_class optional
- active

Avoid unnecessary DOB or other sensitive fields unless a workflow requires them.

## School
Can begin as a parent-created contact record and later be claimed into a workspace.
- id
- name
- timezone
- claimed_workspace_id nullable

## SchoolContact
- id
- school_id
- name
- role/title
- email
- phone optional

## Record / Communication
The central parent-school record.
- id
- family_id
- child_id
- direction: school_to_parent / parent_to_school
- type: notice / acknowledgment / consent / document_request / absence_notice / excuse_letter / general_formal_response
- title
- body or structured summary
- source_type: manual / upload / forwarded_email / school_workspace
- source_attachment_id nullable
- created_by
- created_at

## Action
- id
- record_id
- action_type: read / acknowledge / yes_no / text_response / upload / send_excuse / none
- due_at nullable
- owner_type: parent / delegate / school / none
- owner_id nullable
- status: needs_action / waiting / done / cancelled
- completed_at nullable

## Delivery
- id
- record_id
- recipient_email or school_contact_id
- sent_at
- delivered_at nullable
- opened_at nullable
- failed_at nullable
- provider_metadata minimal

## RecipientResponse
- id
- record_id
- recipient_identity or token reference
- response_type: acknowledged / accepted / declined / needs_info / message
- response_payload minimal
- responded_at

## Attachment
- id
- record_id
- storage_key
- filename
- mime_type
- size
- uploaded_by

## AuditEvent
- id
- actor_type
- actor_id nullable
- record_id nullable
- event_type
- timestamp
- metadata minimal

## Design rules
- never rely on mutable text alone for important status
- record state transitions
- preserve sent snapshots
- do not expose one child/family through another recipient token
- keep deletion/export feasible
