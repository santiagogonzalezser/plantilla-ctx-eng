# create_project

## Usage
- `create_project "<natural-language instructions>" [--name my-project]`

## Intent
Take the user prompt and **scaffold a new project** inside the agent scaffold,
without restating rules. **Honor** `/CLAUDE.md` and `/CONSTITUTION.md` for all
standards (TDD, structure, tests location, coverage, etc.).

## Where to create it
- Create a new directory at: `/<slug-from-name-or-prompt>/`
  - If `--name` is provided, use it (kebab-case).
  - Otherwise derive a short slug from the prompt (kebab-case).
  - If the directory exists and is non-empty, stop and ask for a new name.

## Minimal steps
1. **Parse prompt** → detect stack (e.g., Next.js, Python, etc.).
2. **Scaffold** the project in `/<slug>/` using standard tooling for the detected stack.
3. **Apply repo conventions by reference**:
   - Read `/CONSTITUTION.md` and align the scaffold (tests folder, scripts, etc.).
   - Do **not** restate rules here; just follow them.
4. Create a short `/<slug>/README.md` including:
   - One-line summary of the prompt
   - Quick start (how to run tests / dev server) per detected stack
   - A note that rules are defined at repo root (`/CLAUDE.md`, `/CONSTITUTION.md`)
5. Create an empty `/<slug>/features/` folder (ready for `create_initial` if needed).
6. **Regenerate `/FILETREE.md`** (mandatory).

## Notes
- Keep it **idempotent** and minimal. Don’t duplicate root `CLAUDE.md` / `CONSTITUTION.md`; reference them.
- If the prompt is ambiguous, choose conservative defaults and add an **Open Questions** section at the bottom of the project README.
- No extra ceremony: CI, coverage, detailed configs, etc. are governed by `/CONSTITUTION.md` and can be added later by feature pipeline commands.

## Output
- A new project under `/projects/<slug>/` that boots with the chosen stack.
- Updated `/FILETREE.md`.