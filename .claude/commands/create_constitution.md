# create_constitution

## Usage
- `create_constitution "<prompt or requirements>"`  (inline)
- or `create_constitution --from requirements.md`   (file path)

## Goal
Create (or overwrite) a compact `/CONSTITUTION.md` containing **non-negotiable rules**:
TDD, language/stack, folder layout, testing location/patterns, coverage thresholds,
design paradigms, schema/validation, CI gates, and the **FILETREE.md update mandate**.

## Inputs to Load (if present)
- `/CLAUDE.md` (agent ops)
- `/FILETREE.md` (current map)
- Any prior `/CONSTITUTION.md` (merge & tighten)
- Optional requirements file passed via `--from`

## Output
- Write `/CONSTITUTION.md` (overwrite). Keep it **short, bullet-first**.
- Echo a one-line summary of key gates (tests/coverage/CI) into `features/*/RESULT.md` upon next `execute_prp`.

## Template (use defaults if prompt is vague)
Write the Constitution using this compact structure; fill with repo-appropriate defaults inferred from codebase and/or the provided prompt.

---
# CONSTITUTION (non-negotiable)

## Scope
- This file defines **hard rules**. Agents must comply or stop and report blockers.

## Language & Tooling
- Language: **TypeScript** (strict). No `any` without justification.
- Lint/Format: ESLint + Prettier (project config).
- Package manager: infer from repo (`pnpm`/`npm`/`yarn`) and stick to it.

## Architecture & Layout
- Follow **Atomic Design** (atoms → molecules → organisms → templates → pages) if UI exists.
- Canonical folders (adapt if project differs):
  - `app/` or `src/` for application code
  - `components/` split by atomic tiers (if UI)
  - `lib/` for domain/utils; `hooks/`; `types/`
  - `features/feature_00X_*` for specs
  - **Tests** live in `app/tests/` (or `src/tests/`) only

## Testing (TDD)
- **TDD**: write/extend tests **first**, then implement, then refactor.
- Location: `app/tests/` (or `src/tests/` if no `app/`).
- Pattern: `*.test.ts` / `*.test.tsx` (deterministic, no network unless mocked).
- **Coverage thresholds** (minimums): statements 85%, branches 75%, lines 85%, functions 85%.
- Tests must pass and coverage must meet thresholds before code is considered complete.

## CI / Quality Gates
- Commands (infer from repo scripts; else use these):
  - `typecheck`: `tsc --noEmit`
  - `lint`: `eslint .`
  - `test`: `vitest run --coverage` or `jest --coverage`
- CI must run: typecheck → lint → tests (with coverage). Fail on any error or below-threshold coverage.

## Feature Pipeline (spec ops)
- Each big feature lives in `features/feature_00X_{title}/` with `INITIAL.md`, `PRP.md`, `RESULT.md`, `ITERATIONS.md`.
- `execute_prp`:
  - Write tests **first** in `app/tests/`
  - Implement to green; refactor safely
  - Append bullets to `RESULT.md` (Implemented / Files / Tests / Notes / Follow-ups)
  - If refining, append an entry in `ITERATIONS.md`
  - **Regenerate `/FILETREE.md`** (≤4 levels + 1–2 line app summary) — mandatory

## Naming & Conventions
- Directories/files: kebab-case; Components: PascalCase; hooks: `useX`.
- Keep modules small; reuse existing utilities/components; avoid duplication.
- Accessibility and error handling are required when applicable.

## Dependencies
- Prefer stable, documented libraries; pin major versions when introducing new deps.
- Document any new dependency with a link in `RESULT.md`.

## Breaking Changes
- If a rule must be broken, stop, note rationale in the feature’s `RESULT.md`, and request approval (human).

---

## Notes
- Keep Constitution concise; prefer bullets to prose.
- If inputs conflict, **Constitution overrides** `CLAUDE.md`.