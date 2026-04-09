Update documentation after code changes.

## 1. Identify Changes
- Check git diff or recent commits for modified files
- Identify which services/components were changed
- Note any new files, deleted files, or renamed files

## 2. Verify Current Implementation
**CRITICAL**: DO NOT trust existing documentation. Read the actual code and configs.

For each changed file:
- Read the current implementation
- Understand actual behavior (not documented behavior)
- Note any discrepancies with existing docs

## 3. Update Relevant Documentation

- **CHANGELOG.md** (if it exists): Add entry under "Unreleased" section
  - Use categories: Added, Changed, Fixed, Security, Removed
  - Be concise, user-facing language

- **Architecture docs**: Update if the change affects architecture, infrastructure, or system design

- **Onboarding/setup docs**: Update if the change affects setup procedures or operational checklists

- **README.md**: Update if the change affects how the project is used or configured

## 4. Documentation Style Rules

✅ **Concise** — sacrifice grammar for brevity
✅ **Practical** — examples over theory
✅ **Accurate** — code verified, not assumed
✅ **Current** — matches actual implementation

❌ No enterprise fluff
❌ No outdated information
❌ No assumptions without verification

## 5. Ask if Uncertain

If you're unsure about intent behind a change or its impact, **ask me** — don't guess.
