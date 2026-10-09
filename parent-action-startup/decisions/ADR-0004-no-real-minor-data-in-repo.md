# ADR-0004 — No real minor/customer data in repository

## Status
Accepted.

## Decision
All committed fixtures are synthetic. `local_data/` is gitignored for private local experiments. Production/customer data must never be copied into Git.

## Rationale
The product concerns minors and family/school relationships. Repository hygiene must be strict from the beginning.
