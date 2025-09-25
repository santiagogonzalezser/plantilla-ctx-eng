# Create PRP

## Feature folder (argument): $ARGUMENTS
- Expected path: `/features/$ARGUMENTS`
- Read: `/features/$ARGUMENTS/INITIAL.md`
- Write (overwrite): `/features/$ARGUMENTS/PRP.md`

### Preconditions
- If `/features/$ARGUMENTS/INITIAL.md` does not exist, stop and explain the missing file.
- If `features/templates/PRP_base.md` exists, use it as the structural template; otherwise, follow the sections below.

### Inputs to Load (for context)
- `/features/$ARGUMENTS/INITIAL.md`  (required)
- `/CLAUDE.md`  (project rules and conventions)
- `/CONSTITUTION.md`  (non-negotiable contracts; TDD, tests in `app/tests/`, etc.)
- `/FILETREE.md`  (current repo map, if present)
- Optionally inspect recent feature folders for similar patterns (latest `/features/feature_*`).

---

## Goal
Generate a complete **PRP** for general feature implementation with **thorough research**. The PRP must include all necessary context so the AI agent can self-validate and iterate effectively.

Assume the AI agent:
- Has access to the codebase.
- Has the same knowledge cutoff as you.
- **Has web search capabilities** → include URLs to official documentation and examples where relevant.

---

## Research Process

1. **Codebase Analysis**
   - Search for similar features/patterns in the codebase.
   - Identify files to reference in the PRP (paths + brief why they’re relevant).
   - Note existing conventions to follow (naming, atomic structure, styling).
   - Check existing **test** patterns (how tests are structured in `app/tests/`) for validation approach.

2. **External Research**
   - Search for similar implementations and patterns online.
   - Library documentation (include **specific URLs/sections**).
   - Implementation examples (GitHub / StackOverflow / blogs) with links.
   - Best practices and common pitfalls (call out version specifics if applicable).

3. **User Clarification** (if needed)
   - List any open questions that block implementation (patterns, integrations, data sources).
   - Keep this section short and actionable.

---

## PRP Generation
Use `features/templates/PRP_base.md` as a template **if present**; otherwise, compose the PRP with the following sections:

### Critical Context (pass this to the AI agent verbatim)
- **Documentation**: URLs with specific sections/anchors.
- **Code Examples**: Real snippets from the current codebase (cite file paths).
- **Gotchas**: Library quirks, version constraints, edge cases.
- **Patterns**: Existing approaches to follow (atomic design, folder rules from `CLAUDE.md`/`CONSTITUTION.md`).

### Implementation Blueprint
- High-level pseudocode outlining the approach.
- References to real files for patterns (e.g., “mirror `components/ui/Button.tsx` API”).
- Error handling strategy and failure modes.
- **Ordered task list** to fulfill the PRP end-to-end (TDD first: write/extend tests in `app/tests/`, then implement, then refactor).

> **CRITICAL BEFORE WRITING**  
> After researching and exploring the codebase, **think deeply** about the plan, validate it against `CLAUDE.md` and `CONSTITUTION.md`, then write the PRP.

---

## Output
- Save the PRP to: `/features/$ARGUMENTS/PRP.md` (overwrite if it exists).
- Do **not** print the full PRP to chat; write the file.

---

## Quality Checklist (include at end of PRP)
- [ ] All necessary context included (internal + external)
- [ ] Validation gates executable by AI (tests first; `app/tests/`)
- [ ] References to existing patterns and files
- [ ] Clear, ordered implementation path
- [ ] Error handling documented
- [ ] Aligned with `CLAUDE.md` and `CONSTITUTION.md`

**Confidence Score**  
Give a 1–10 confidence score: “Likelihood of one-pass implementation by Claude Code given this PRP.”

---

## Notes
- Preserve numbering and title from `$ARGUMENTS` (e.g., `feature_001_hero-section`).
- Keep the PRP concise but **complete**. Prefer links + tight snippets over long quotations.
- If a section cannot be completed (e.g., missing tests baseline), state the gap explicitly and propose the minimal addition.