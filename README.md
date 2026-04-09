# Claude Code Project Template

A ready-to-clone project template for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that gives you a structured development workflow, custom slash commands, and sensible defaults from day one.

**Author:** Walter Varma-Chang
**License:** MIT
**Created:** April 2026

## What This Is

This template captures a battle-tested Claude Code setup — the `CLAUDE.md` project instructions, custom commands, and permission configs that make Claude Code actually useful for building software. Instead of re-configuring Claude Code for every new project, clone this and customize.

It includes:

- **`CLAUDE.md`** — Project instructions template with placeholders for your project details, tech stack, deployment workflow, and coding standards
- **`.claude/`** — Permission settings and 12 custom slash commands covering the full dev lifecycle: explore → plan → execute → review → deploy → document
- **`docs/`** — A place for your canonical project documents (architecture specs, onboarding guides, etc.)
- **`sred/`** — Optional SR&ED (Scientific Research & Experimental Development) tax credit documentation structure for Canadian companies doing R&D
- **`/onboard`** — A guided setup command that walks you through customizing the template for your project

## Who This Is For

Developers and technical founders who use Claude Code and want a consistent, repeatable project setup. You should be comfortable with:

- Git and GitHub
- Terminal / command line
- Reading and editing Markdown
- The basics of how Claude Code works

## Quick Start

```bash
# Clone the template
git clone https://github.com/wally-msl/claude-project-template.git my-project
cd my-project

# Remove the template's git history and start fresh
rm -rf .git
git init

# Open in Claude Code and run the onboarding command
claude
# Then type: /onboard
```

The `/onboard` command will walk you through customizing `CLAUDE.md` for your project.

## What You Should Bring

This template gives you the *workflow*. You supply the *context*. The more project context you give Claude Code via `CLAUDE.md` and docs, the better it performs. We recommend having (or creating) these for your project:

- **A project brief or seed document** — What you're building, why, key architectural decisions, governance model if applicable. This is the "what" and "why" of your project.
- **A technical architecture document** — Tech stack, infrastructure, deployment model, data model, integrations. This is the "how" of your project.
- **An onboarding guide** (optional) — How to set up the development environment, deploy, access services. Useful if you're onboarding collaborators or future-you.

These go in `docs/` and get referenced from `CLAUDE.md`. You don't need all of them on day one — start with whatever you have and add more as your project takes shape.

## Template Structure

```
claude-project-template/
├── README.md                              # This file
├── CLAUDE.md                              # Project instructions (customize this)
├── .claude/
│   ├── settings.local.json                # Permission allowlists
│   └── commands/
│       ├── onboard.md                     # Guided setup wizard
│       ├── explore.md                     # Investigate before implementing
│       ├── create-plan.md                 # Generate execution plans
│       ├── execute.md                     # Implement from a plan
│       ├── review.md                      # Code review checklist
│       ├── deploy.md                      # Deploy to server
│       ├── document.md                    # Update docs after changes
│       ├── create-issue.md                # Quick issue capture
│       ├── save-recipe.md                 # Document solutions for reuse
│       ├── learning-opportunity.md        # Pause to learn a concept
│       ├── peer-review.md                 # Evaluate external review findings
│       └── sred-log.md                    # SR&ED documentation (optional)
├── docs/
│   ├── README.md                          # What goes in this folder
│   ├── plans/                             # Execution plans (auto-generated)
│   └── recipes/                           # Reusable solutions (auto-generated)
│       └── README.md                      # Recipe format guide
└── sred/                                  # SR&ED documentation (optional)
    └── README.md                          # SR&ED setup instructions
```

## The Command Workflow

The custom commands are designed to work together as a development lifecycle:

```
/explore  →  /create-plan  →  /execute  →  /review  →  /deploy  →  /document
                                  ↑                                      │
                                  └──────────────────────────────────────┘
```

**`/onboard`** — Run once when you first clone the template. Walks you through customizing CLAUDE.md.

**`/explore`** — Investigate before building. Claude reads the codebase, checks current state, identifies dependencies, and asks clarifying questions. No code gets written.

**`/create-plan`** — Produce a tracked execution plan with steps, status emojis, and progress percentage. Plans are saved to `docs/plans/` as timestamped markdown files.

**`/execute`** — Implement from a plan. Claude follows the plan step by step, updates progress tracking, and runs verification after each step.

**`/review`** — Code review against a configurable checklist (security, code quality, infrastructure, etc.). Outputs findings by severity.

**`/deploy`** — Stage, commit, push, and deploy to your server. Verifies health after deployment.

**`/document`** — Update documentation to match what was actually built. Reads the real code, not assumptions.

**`/create-issue`** — Quick issue capture when you're mid-flow. Asks minimal questions, creates a structured issue.

**`/save-recipe`** — Document a solution you just figured out so you don't solve it again.

**`/learning-opportunity`** — Pause to understand a concept at three levels of depth.

**`/peer-review`** — Critically evaluate findings from another tool or reviewer against your project's actual architecture.

**`/sred-log`** — (Optional) Document work for Canadian SR&ED tax credits with contemporaneous evidence.

## Customization Guide

### CLAUDE.md

This is the most important file. It tells Claude Code who you are, what you're building, and how you work. The template has clearly marked `[PLACEHOLDER]` sections — fill these in:

- **Project Overview** — What you're building
- **Who I Am** — Your technical level and working style
- **Tech Stack** — Your actual technologies
- **Architecture Decisions** — Key design choices Claude should respect
- **Development Workflow** — How code gets from your machine to production
- **Deployment Details** — SSH targets, paths, scripts
- **Code Style** — Languages, conventions, patterns

### .claude/settings.local.json

The default permissions allow git operations and SSH. Add your own server hostnames and any other commands you want Claude to run without asking:

```json
{
  "permissions": {
    "allow": [
      "Bash(git:*)",
      "Bash(ssh your-user@your-server:*)"
    ]
  }
}
```

### Custom Commands

Every command in `.claude/commands/` is a markdown file. Edit them freely — add project-specific checklists, change review criteria, adjust the plan template. You can also add new commands by creating new `.md` files in that directory.

## SR&ED Module (Optional)

If you're a Canadian corporation doing R&D, the `sred/` directory and `/sred-log` command help you maintain contemporaneous documentation for SR&ED tax credit claims. This is the strongest form of evidence for CRA — records created as the work happens, not reconstructed afterward.

The setup:

1. Define your experimental hypotheses in `CLAUDE.md`
2. Use `/sred-log` after completing experimental work
3. Git commit timestamps provide the chronological proof
4. The `/create-plan` and `/execute` commands automatically prompt for SR&ED pre/post logging when work is tagged as relevant

See `sred/README.md` for detailed setup instructions.

For SR&ED claim preparation (discovery, interviews, filing), consider building Claude Cowork skills that integrate with this template's documentation structure. See the Cowork skills documentation for guidance.

## Tips

- **Start with `/onboard`** — it takes 5 minutes and makes everything else work better.
- **Keep CLAUDE.md current** — when your architecture changes, update it. Claude Code is only as good as the context you give it.
- **Use `/explore` before `/create-plan`** — the explore step catches assumptions and edge cases before you commit to an approach.
- **Commit plans before executing** — plans in `docs/plans/` with git timestamps are useful project history (and SR&ED evidence if applicable).
- **Let recipes accumulate** — the `/save-recipe` and auto-recipe detection in `/execute` build a project-specific knowledge base over time.

## Contributing

Issues and PRs welcome. This template reflects one workflow — if you've found patterns that work well with Claude Code, share them.

## License

MIT — use it however you want.
