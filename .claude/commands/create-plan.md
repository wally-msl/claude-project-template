Based on our full exchange, produce a markdown execution plan.

Requirements for the plan:

- Include clear, minimal, concise steps.
- Track the status of each step using these emojis:
  - 🟩 Done
  - 🟨 In Progress
  - 🟥 To Do
- Include dynamic tracking of overall progress percentage (at top).
- Do NOT add extra scope or unnecessary complexity beyond what we discussed.
- Steps should be modular and integrate seamlessly within the existing project.

For each step, note:
- Which service/component is affected
- Whether a deploy is needed
- Whether secrets or environment variables need updating

Markdown Template:

# Implementation Plan: [Feature/Change Name]

**Overall Progress:** `0%`

## TLDR
Short summary of what we're building and why.

## Critical Decisions
Key architectural/implementation choices made during exploration:
- Decision 1: [choice] - [brief rationale]
- Decision 2: [choice] - [brief rationale]

## Tasks:

- [ ] 🟥 **Step 1: [Name]** [component: X]
  - [ ] 🟥 Subtask 1
  - [ ] 🟥 Subtask 2

- [ ] 🟥 **Step 2: [Name]** [component: X]
  - [ ] 🟥 Subtask 1
  - [ ] 🟥 Subtask 2

## Deploy Checklist
- [ ] Commit with descriptive message
- [ ] Push to GitHub
- [ ] Deploy (follow project-specific deploy process)
- [ ] Verify affected services are healthy

It's still not time to build yet. Just write the clear plan document.

Save the plan as a markdown file in docs/plans/ with the naming convention YYYY-MM-DD-[slug].md. Commit it with the message 'Plan: [feature/change name]'.
