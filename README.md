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

## Starting a New Project

### Step 1: Think through your project first

Before touching Claude Code, use a Claude Chat project (or ChatGPT, or whatever you think with) to work through your project's architecture. Have a conversation covering what you're building, who it's for, tech stack choices, key design decisions, and how you'll deploy it. Then ask it to produce:

- **A project brief or seed document** — What you're building, why, key architectural decisions, governance model if applicable. The "what" and "why."
- **A technical architecture document** — Tech stack, infrastructure, deployment model, data model, integrations. The "how."
- **An onboarding guide** (optional) — How to set up the dev environment, deploy, access services. Useful for future-you or collaborators.

You don't need a specific prompt template for these — the quality comes from the back-and-forth conversation, not from a single prompt. Start with whatever you have and add more as your project takes shape.

### Step 2: Clone the template

```bash
git clone https://github.com/wally-msl/claude-project-template.git my-project
cd my-project
rm -rf .git
git init
```

### Step 3: Drop in your seed docs

Copy whatever project documents you created in Step 1 into the `docs/` folder.

### Step 4: Run the onboarding command

```bash
claude
# Then type: /onboard
```

The `/onboard` command walks you through customizing `CLAUDE.md` — your tech stack, deploy process, SSH targets, architecture decisions. Takes about 5 minutes.

### Step 5: Point CLAUDE.md at your docs

After onboarding, add your documents to the "Current canonical documents" section in `CLAUDE.md` so Claude Code knows they exist and references them when making decisions.

### Step 6: Start building

```
/explore
```

That's it. The template handles the Claude Code setup, your seed docs handle the project context, and you're building from the first session.

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
