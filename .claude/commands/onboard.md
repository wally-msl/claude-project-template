Welcome to your new Claude Code project. Let's get it configured.

## What This Does

Walk through CLAUDE.md and customize it for your project. This takes about 5 minutes and makes every subsequent interaction with Claude Code significantly better.

## Steps

1. **Read the current CLAUDE.md** to understand the template structure.

2. **Ask me these questions one at a time** (don't dump them all at once):
   - What's the project name and a one-sentence description?
   - What's your tech stack? (languages, frameworks, database, infrastructure)
   - How do you deploy? (e.g., SSH to a server, push to Vercel, docker compose up)
   - What are 2-3 key architecture decisions I should respect?
   - Do you have a server I should know how to SSH into? If so, what's the user@host and repo path?
   - Are you doing SR&ED? (Canadian R&D tax credits — skip if unsure)

3. **Update CLAUDE.md** with my answers, replacing all `[PLACEHOLDER]` sections.

4. **Update `.claude/settings.local.json`** if I gave you SSH details — add the server to the permission allowlist:
   ```json
   "Bash(ssh [user]@[host]:*)"
   ```

5. **Show me a summary** of what was configured and what's left to do.

6. **Suggest next steps:**
   - Create a seed document or project brief in `docs/`
   - Try `/explore` to investigate an existing codebase
   - Try `/create-plan` to plan your first feature
   - If doing SR&ED: define hypotheses in CLAUDE.md and see `sred/README.md`

## Tone

Keep it conversational and efficient. Don't over-explain — I chose to use this template, so I'm already bought in. Just help me fill in the blanks.
