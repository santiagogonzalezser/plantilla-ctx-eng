# CLAUDE.md

Authoritative. Manage work via these rules:

- **Feature pipeline**: `create_feature` → `create_prp` → `execute_prp`.
- **Artifacts per feature**: `features/feature_00X_{title}/{INITIAL.md, PRP.md, RESULT.md, ITERATIONS.md}`.
- **Always read** the latest feature’s `RESULT.md` before new work.
- **Always regenerate** `/FILETREE.md` after any code change (≤4 levels + 1–2 line app summary).
- **TDD is enforced in the Constitution**; follow it strictly.
- Prefer small, composable changes; reuse existing components; avoid duplication.
- If requirements are unclear, write short “Open Questions” in `RESULT.md` and proceed with the safest minimal implementation.