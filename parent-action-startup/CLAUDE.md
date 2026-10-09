# CLAUDE.md

Claude Code: use `AGENTS.md` as the canonical instructions.

At the start of a session, read:
- `AGENTS.md`
- `docs/STATUS.md`
- `docs/ROADMAP.md`
- relevant `specs/`
- recent `decisions/`

Do not rely on previous chat memory as project truth.

For ambiguous requests, first compare them against `docs/PRODUCT.md` and `docs/PRODUCT_PRINCIPLES.md`. Flag scope creep before implementing it.

Do not use real child/school data in fixtures. Use `data/synthetic/` only.
