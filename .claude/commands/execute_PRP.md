# Execute PRP

## Feature folder (argument): $ARGUMENTS
- Expected path: `/features/$ARGUMENTS`
- Read (required): `/features/$ARGUMENTS/PRP.md`
- Also read (if present): `/features/$ARGUMENTS/INITIAL.md`, `/features/$ARGUMENTS/RESULT.md`, `/features/$ARGUMENTS/ITERATIONS.md`
- Write/update:
  - Code under `/app/` (and `/components`, `/lib`, etc. per CLAUDE.md)
  - Tests under `/app/tests/`
  - `/features/$ARGUMENTS/RESULT.md` (append bullet points)
  - `/features/$ARGUMENTS/ITERATIONS.md` (append entry if this is a refinement)
  - `/FILETREE.md` (regenerate)

### Preconditions
- If `/features/$ARGUMENTS/PRP.md` does not exist, **stop** and explain the missing file.
- If `/features/$ARGUMENTS/RESULT.md` or `ITERATIONS.md` do not exist, create them with `# RESULT` / `# ITERATIONS` headers.
- Enforce `/CONSTITUTION.md` (TDD; tests live in `app/tests/`) and follow `/CLAUDE.md` (atomic design, structure, styling).
- Use the latest repo state described in `/FILETREE.md` if present.

### Inputs to Load (for context)
- `/features/$ARGUMENTS/PRP.md`  (required source of truth)
- `/CLAUDE.md`                  (project rules and conventions)
- `/CONSTITUTION.md`            (non-negotiable contracts; TDD, tests in `app/tests/`, etc.)
- `/FILETREE.md`                (current repo map, if present)
- Optionally inspect recent `features/feature_*` for analogous patterns.

---

## Goal
**Implement** the feature described by the PRP using **Test-Driven Development**:
1) write/extend tests in `app/tests/`,  
2) implement code to make tests pass,  
3) refactor if needed while keeping tests green.  
Then update `RESULT.md`, append to `ITERATIONS.md` (if re-run), and regenerate `FILETREE.md`.

---

## Execution Plan

1. **Understand & Validate the PRP**
   - Extract the ordered task list and acceptance criteria.
   - Cross-check with `CLAUDE.md` (atomic layers, placement, naming) and `CONSTITUTION.md` (TDD, TS, Tailwind/shadcn rules).
   - If the PRP conflicts with the constitution/rules, document the mismatch in `RESULT.md` and align the approach.

2. **TDD – Author/Extend Tests First**
   - Derive concrete test cases from PRP acceptance criteria (unit + integration where appropriate).
   - Create/extend tests under `app/tests/` using filename pattern:  
     `app/tests/${ARGUMENTS}.test.tsx` (or multiple files if clearer).
   - Include edge cases and error paths specified in the PRP.
   - The initial test run should **fail** by design (pre-implementation).

3. **Implement the Feature**
   - Implement only what is required to make the tests pass.
   - Follow **Atomic Design** and the folder conventions in `CLAUDE.md`.
   - Respect type safety (TypeScript strict), a11y, and performance considerations called out in the PRP.
   - Reuse existing atoms/molecules/organisms when possible; don’t duplicate patterns.

4. **Refactor with Safety**
   - After tests pass, refactor for readability/composition while keeping tests green.
   - Update or add minimal docs/comments when it increases clarity (keep it tight).

5. **Validation & Health Checks**
   - Ensure **all tests pass** (`app/tests/`).
   - Run type checks and lint rules if available; fix any issues.
   - Confirm Next.js routes/components render paths match PRP expectations.

6. **Update Feature Artifacts**
   - **RESULT.md** (append bullet points):  
     - What was implemented (short, action-style bullets)  
     - Files created/modified (paths)  
     - Tests added/updated (paths)  
     - Notes (e.g., tradeoffs, follow-ups)
   - **ITERATIONS.md**: if this is not the first run, append an entry:
     ```
     ## Iteration N – YYYY-MM-DD
     - Prompt/goal of iteration
     - Summary of fixes/changes
     - Impact on tests/code
     ```
   - **FILETREE.md**: regenerate a concise repo tree (up to 4 levels) and a 1–2 line app summary. Replace the file.

---

## Output
- Implemented code under `/app/…` (and related folders).
- Tests under `/app/tests/…` that assert acceptance criteria.
- Updated `/features/$ARGUMENTS/RESULT.md` (bullet list).
- Updated `/features/$ARGUMENTS/ITERATIONS.md` (if applicable).
- Regenerated `/FILETREE.md`.

> **Idempotency:** Re-running `execute_prp` on the same `$ARGUMENTS` should treat it as a refinement pass: only incremental changes, append to `ITERATIONS.md`, and extend `RESULT.md` bullets.

---

## Quality Checklist (verify before finishing)
- [ ] Tests exist in `app/tests/` and **pass** locally.
- [ ] Type checks and lint pass (if configured).
- [ ] Adheres to `CLAUDE.md` (structure, atomic design, styling) and `CONSTITUTION.md` (TDD, contracts).
- [ ] RESULT.md updated with clear bullet points + file paths.
- [ ] ITERATIONS.md appended if this was a refinement.
- [ ] FILETREE.md regenerated and accurate.
- [ ] No dead code, duplicated components, or violations of patterns.

---

## Notes
- Preserve the feature folder name and numbering (e.g., `feature_001_hero-section`).
- Keep diffs minimal and focused on PRP scope.
- If blockers arise (missing APIs, unclear requirements), document in `RESULT.md` under **Blockers** and propose the minimal next step.