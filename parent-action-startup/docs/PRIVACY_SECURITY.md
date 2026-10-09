# Privacy and Security Working Requirements

This product handles information about minors and family relationships. Treat privacy as core product design, not a launch checklist.

## Data minimization
Only collect data required to identify the child, school context, action, delivery, and response.

Avoid collecting by default:
- full medical history
- diagnoses
- academic performance
- behavior records
- government IDs
- unnecessary DOB
- unrelated family data

For absence reporting, prefer categories such as:
- illness
- appointment
- family matter
- travel
- other

Free-text detail should be optional.

## Repository rules
- no real student/guardian/school data in Git
- no copied production attachments in local fixtures
- `data/synthetic/` only for committed examples
- `local_data/` for private experiments; never commit

## Access model
- parent sees only their family data
- delegate permissions are explicit
- secure recipient links expose only the individual record required
- school workspaces later require tenant isolation and role-based access

## Security requirements before pilot
- secure authentication
- email verification
- session management
- signed/expiring recipient tokens
- attachment authorization
- encrypted transport
- managed secret storage
- audit events for sensitive transitions
- abuse/rate limiting
- deletion/export workflows
- backups and restoration plan

## Legal research backlog
Research applicability before external compliance claims:
- GDPR / UK GDPR
- U.S. state privacy requirements
- COPPA where relevant
- FERPA where school-held education records become involved
- electronic consent/signature requirements by jurisdiction
- data processing agreements for school customers

Do not state “compliant with X” until the exact product flow and legal obligations are reviewed.
