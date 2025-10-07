# Command: git_command <instruction or command>

## Usage
- `/git_command "<natural language description or git command>" [--project <dir>]`
  - Example: `/git_command "initialize repo and push to GitHub" --project my-next-app`
  - Example: `/git_command "git add . && git commit -m 'update ui'" --project python-api`

## Intent
Enable Claude to **interpret or execute Git actions inside a project directory** created under the **current development scaffold** (not at root).  
- Natural language → infer Git commands (`init`, `add`, `commit`, `push`, etc.).  
- Explicit commands → execute them as given inside the target project.  
- If `--project` is missing, Claude must detect or ask for the project directory.

## Preconditions
- Root contains `/CLAUDE.md` and `/CONSTITUTION.md`.  
- Target project folder exists inside current scaffold (e.g., `/<slug>/` or `/next-app/`).  
- `.git/` verified or initialized **inside that project directory**, not at root.  
- Ask for missing data (repo URL, branch name, commit message).

## Execution
1. Identify the project directory (`--project` or inferred).  
2. Change working directory into that project.  
3. Parse intent or direct commands.  
4. Confirm or request missing parameters.  
5. Run sequence safely (`git init` → `add` → `commit` → `push`, etc.).  
6. Create/update `/features/feature_00X_git-command/RESULT.md` summarizing actions and paths.

## Output
- Git actions executed or simulated **inside the specified project**.  
- `.gitignore` created if missing.  
- Confirmation message:  
  `✅ Git command(s) executed successfully in <project>.`

## Notes
- Never push sensitive files (`.env`, `config.json`, etc.).  
- Default `.gitignore`: `node_modules/`, `dist/`, `.env`, `.DS_Store`, `coverage/`.  
- Command must be **idempotent and interactive** when ambiguous.  
- Root (`/`) remains a **non-repo scaffold**; Git applies only to **subprojects**.