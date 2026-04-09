# Recipes

Reusable solutions to problems encountered during development. Created by `/save-recipe` or auto-detected by `/execute` when it encounters a non-obvious fix.

## Recipe Format

```markdown
# [Short descriptive title]

**Problem:** What went wrong or what was hard to figure out.

**Context:** What we were doing when this came up. Include versions, OS, tools.

**Solution:** The fix, step by step. Include actual commands or code.

**Why it works:** Brief explanation so future-you understands the reasoning.

**Gotchas:** Anything that might trip you up again.
```

## Examples of Good Recipes

- "SSH PATH not loading on non-interactive sessions" — because you'll forget this in 3 months
- "Docker compose healthcheck for PostgreSQL" — the obvious approach doesn't work
- "SOPS decrypt failing on server" — needs an explicit env var for the key file path

## When to Write a Recipe

If you spent more than 10 minutes debugging something and the fix wasn't obvious from the error message, it's worth a recipe.
