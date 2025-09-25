# CLAUDE.md

Authoritative. Manage work via these rules:

- **Feature pipeline**:  
  `create_feature` → `create_prp` → `execute_prp`.

- **Artifacts per feature**:  
  `features/feature_00X_{title}/{INITIAL.md, PRP.md, RESULT.md, ITERATIONS.md}`.

- **Always read** the latest feature’s `RESULT.md` before new work.

- **Always regenerate** `/FILETREE.md` after any code change:  
  - Format as a **Markdown text file** (never binary).  
  - Use a fenced code block with a directory tree (≤4 levels).  
  - Add a **1–2 line summary** below each project root directory.  
  - Example:

    ```markdown
    # FILETREE

    ```
    /
    ├── CLAUDE.md
    ├── CONSTITUTION.md
    ├── next-app/                # Next.js project with shadcn UI
    │   ├── README.md
    │   ├── features/
    │   ├── src/
    │   │   ├── app/
    │   │   └── components/
    │   └── tests/
    └── python-api/              # Python FastAPI service
        ├── README.md
        ├── features/
        ├── app/
        └── tests/
    ```

- Prefer small, composable changes; reuse existing components; avoid duplication.

- If requirements are unclear, write short “Open Questions” in `RESULT.md` and proceed with the safest minimal implementation.