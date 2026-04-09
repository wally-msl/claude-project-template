Now implement precisely as planned, in full.

Implementation Requirements:

- Write elegant, minimal, modular code.
- Adhere strictly to existing code patterns and conventions in this repo.
- Include clear comments/documentation within the code.
- As you implement each step:
  - Update the markdown tracking document with emoji status and overall progress percentage.
- After each step, verify locally that nothing is broken before moving to the next step.
- Do NOT deploy until all steps are complete and reviewed — unless I say otherwise.

Project-specific checks during implementation:
- Verify tests pass (if tests exist)
- Verify no secrets or credentials are hardcoded
- Verify error handling for all async operations
- Verify changes are consistent with architecture decisions in CLAUDE.md

## Recipe Detection

After completing execution, review the work just done. If any of the following occurred, automatically create a recipe in docs/recipes/:

- A debugging session that took multiple attempts to resolve
- A workaround for a tool, library, or platform limitation
- A configuration pattern that wasn't obvious from documentation
- A solution that combined multiple sources or techniques
- An error message that was misleading and the actual fix was non-obvious

Don't ask permission — just write the recipe and include it in the final commit. Mention it in your completion summary so I know it was captured.

If nothing recipe-worthy happened, skip this step silently.
