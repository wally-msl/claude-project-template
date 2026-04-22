# Claude Code Project Template

This is not just a [Claude Code](https://docs.anthropic.com/en/docs/claude-code) starter.

It is a product development operating system for building with AI.

The goal is simple: encode how experienced product teams work into the way the model operates.

Instead of relying on better prompts, this template shapes:

- what the model sees before it starts
- how it approaches problems
- how work is planned, executed, reviewed, and documented

At the center is a lifecycle:

`/explore → /create-plan → /execute → /review → /deploy → /document`

Every meaningful change flows through this loop.

The result is not just faster output. It is more consistent, reviewable, and understandable work.

**Author:** Walter Varma-Chang
**License:** MIT
**Created:** April 2026

## Why this template is different

Most AI workflows optimize for output.

This template optimizes for how the work happens.

It is designed to prevent common failure modes:

- **Building before understanding the problem.** `/explore` forces investigation before any implementation begins — it opens with *"Do NOT implement yet."*
- **Losing track of decisions and progress.** `/create-plan` turns work into an explicit, trackable plan — a markdown artifact with status emojis and a progress percentage, committed to `docs/plans/`.
- **Forgetting hard-won debugging knowledge.** `/execute` captures non-obvious fixes as reusable recipes in `docs/recipes/` automatically. Institutional memory accumulates instead of evaporating.
- **Blindly trusting reviewer feedback or model output.** `/peer-review` verifies findings against the real code before accepting them, instead of treating them as a checklist.
- **Letting documentation drift from reality.** `/document` reads the actual code and configuration before writing anything. The source of truth is the repo, not the prose.

An optional R&D evidence module (`/sred-log`, `sred/`) adds contemporaneous logging for teams that need to reconstruct *why* research work was done — originally designed for Canadian SR&ED claims, useful anywhere that kind of audit trail matters.

The goal is not just to move faster. It is to make the work more deliberate, inspectable, and repeatable.

## Review before adoption

Treat this like any third-party starter: inspect it, adapt it, and keep only what fits your workflow.

This repo is intentionally opinionated. Some parts will be useful immediately. Others may not fit how you work.

Before using it in a real project, it is worth asking your coding agent to review it:

- Are there any potential security risks?
- Does the workflow align with how you already work?
- What can be simplified or removed?

A useful prompt:

> Review this repository as a senior engineer and product operator. Identify any security risks, unnecessary complexity, or workflow assumptions that may not fit my use case. Recommend what to keep, modify, or remove.

See `AGENTS.md` at the repo root for a more structured version of this review, written to be handed directly to another LLM.

The goal is not blind adoption. The goal is selective adoption with judgment.

## Who This Is For

Builders who use Claude Code and want a repeatable workflow rather than a clean terminal. Comfort with Git, the terminal, and Markdown is assumed. Non-technical founders who can read code or configs will get value — you're reviewing the AI's work, not writing it yourself.

## Seed Documents: What Claude Sees Before It Starts

The commands are only as good as the context they run against. Before you start building, give Claude Code a small set of high-signal documents in `docs/`:

- **Project brief / seed document** — what you're building and why. The vision, constraints, and non-goals.
- **Technical architecture document** — tech stack, infrastructure, data model, deployment. The "how."
- **Onboarding guide** (optional) — how to set up the dev environment, deploy, access services. Useful for future-you or collaborators.

These are what `/explore` reads before it investigates, what `/create-plan` respects when it proposes steps, and what `/document` treats as source of truth alongside the code. You don't need a specific prompt template for them — the quality comes from thinking the project through in a Claude Chat project (or ChatGPT, or a whiteboard) and producing rough-but-real artifacts. An empty `docs/` folder is a weak foundation; a half-page brief is already enough.

See `examples/` for minimal versions of each.

## Starting a New Project

### Step 1: Think through the project first

Have a conversation somewhere (Claude Chat project, ChatGPT, a co-founder) covering what you're building, who it's for, tech stack choices, key design decisions, and how you'll deploy. Ask it to produce a project brief and a technical architecture doc. They don't need to be polished — they need to exist.

### Step 2: Clone the template

```bash
git clone https://github.com/wally-msl/claude-project-template.git my-project
cd my-project
rm -rf .git
git init
```

### Step 3: Drop in your seed docs

Copy whatever you produced in Step 1 into the `docs/` folder.

### Step 4: Run the onboarding command

```bash
claude
# Then type: /onboard
```

The `/onboard` command walks you through customizing `CLAUDE.md` — your tech stack, deploy process, SSH targets, architecture decisions. Takes about 5 minutes.

### Step 5: Point CLAUDE.md at your docs

After onboarding, add your documents to the "Current canonical documents" section in `CLAUDE.md` so Claude Code references them when making decisions.

### Step 6: Start building

```
/explore
```

## Template Structure

```
claude-project-template/
├── README.md                              # This file
├── AGENTS.md                              # Lens for another LLM reviewing your workflow
├── CLAUDE.md                              # Project instructions (customize this)
├── .claude/
│   ├── settings.local.json                # Permission allowlists
│   └── commands/
│       ├── onboard.md                     # Guided setup wizard
│       ├── explore.md                     # Investigate before implementing
│       ├── create-plan.md                 # Generate tracked execution plans
│       ├── execute.md                     # Implement from a plan (+ recipe capture)
│       ├── review.md                      # Code review checklist
│       ├── deploy.md                      # Deploy to server
│       ├── document.md                    # Update docs grounded in real code
│       ├── create-issue.md                # Quick issue capture
│       ├── save-recipe.md                 # Document solutions for reuse
│       ├── learning-opportunity.md        # Pause to learn a concept
│       ├── peer-review.md                 # Verify external review findings
│       └── sred-log.md                    # R&D evidence capture (optional)
├── docs/
│   ├── README.md                          # What goes in this folder
│   ├── plans/                             # Execution plans (generated)
│   └── recipes/                           # Reusable solutions (generated)
├── examples/                              # Minimal sample artifacts
│   ├── README.md
│   ├── plans/
│   ├── recipes/
│   ├── seed-docs/
│   └── sred/
└── sred/                                  # R&D evidence (optional)
    └── README.md
```

## The Commands

### Core Lifecycle

**`/explore`** — Investigate before building. Claude reads the codebase, checks current state, identifies dependencies, and asks clarifying questions. Starts with *"Do NOT implement yet."* No code gets written in this step.

**`/create-plan`** — Produce a tracked execution plan with steps, status emojis, and a progress percentage. Plans are saved to `docs/plans/` as timestamped markdown files and committed to git. The plan is the artifact, not the chat history.

**`/execute`** — Implement from a plan. Claude follows the plan step by step, updates progress tracking, verifies after each step, and automatically captures non-obvious fixes as recipes in `docs/recipes/`.

**`/review`** — Code review against a configurable checklist (security, code quality, infrastructure, tests). Outputs findings by severity.

**`/deploy`** — Stage, commit, push, and deploy to your server. Verifies health after deployment.

**`/document`** — Update documentation to match what was actually built. Explicitly instructed to distrust existing docs and read the real code.

### Supporting Commands

**`/onboard`** — One-time wizard to customize `CLAUDE.md` for your project.

**`/create-issue`** — Fast issue capture mid-flow. Minimal questions, structured output.

**`/save-recipe`** — Manually capture a solution you just figured out.

**`/learning-opportunity`** — Pause development and explain a concept at three levels of depth.

**`/peer-review`** — Critically evaluate findings from another tool or reviewer. Verifies each finding against the actual code before accepting it.

**`/sred-log`** — Optional. Write a contemporaneous R&D evidence entry for the work you just did.

## Customization Guide

### Keep sensitive details out of tracked files

`CLAUDE.md`, `docs/`, and `sred/` are all committed to git. Do not put real SSH hostnames, internal URLs, server paths, customer names, or credentials into them — especially if the repo is or will ever be public. The template intentionally uses placeholders like `[user]@[hostname]` for this reason.

For anything environment-specific, use one of:

- `.claude/settings.local.json` — already in `.gitignore` in most setups; good for per-machine permission allowlists
- `.env.local` — already ignored; good for runtime secrets
- Shell config or a password manager — good for SSH targets and deploy credentials
- A separate, private repo or encrypted file (SOPS, age, Vault) — good for anything you want versioned but not exposed

The onboarding wizard (`/onboard`) will ask for deploy details. Give it placeholders rather than real values if you're unsure where the repo will end up.

### CLAUDE.md

The most important file. It tells Claude Code who you are, what you're building, and how you work. Template has clearly marked `[PLACEHOLDER]` sections — fill these in:

- **Project Overview** — what you're building
- **Who I Am** — your technical level and working style
- **Tech Stack** — your actual technologies
- **Architecture Decisions** — key choices Claude should respect
- **Development Workflow** — how code gets from your machine to production
- **Deployment Details** — SSH targets, paths, scripts (see the warning above before pasting real values)
- **Code Style** — languages, conventions, patterns

### .claude/settings.local.json

Default permissions allow git operations and SSH. Add your own server hostnames and any other commands you want Claude to run without prompting:

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

Every command in `.claude/commands/` is a markdown file. Edit them — add project-specific checklists, tighten review criteria, adjust the plan template. Create new commands by dropping new `.md` files in that directory.

## Optional: R&D Evidence Logging (SR&ED)

The `sred/` directory and `/sred-log` command capture contemporaneous records of experimental work. This was designed for Canadian [SR&ED](https://www.canada.ca/en/revenue-agency/services/scientific-research-experimental-development-tax-incentive-program.html) claims, where "created as the work happens" records are the strongest form of evidence — but the pattern is useful beyond Canada. Any team that has ever had to reconstruct the reasoning behind a research direction months later knows the problem this solves.

How it plugs in:

1. Define experimental hypotheses in `CLAUDE.md`
2. Use `/sred-log` after completing experimental work
3. Git commit timestamps provide the chronological proof
4. `/create-plan` and `/execute` prompt for SR&ED pre/post logging when work is tagged as relevant

If you don't need it, delete `sred/` and remove the corresponding section from `CLAUDE.md`. The rest of the template doesn't depend on it.

See `sred/README.md` for setup. For claim preparation (discovery, interviews, filing), consider building Claude Cowork skills that integrate with this template's documentation structure.

## Tips

- **Start with `/onboard`** — five minutes that make every other command work better.
- **Keep CLAUDE.md current** — when your architecture shifts, update it. Claude is only as good as the context you feed it.
- **Use `/explore` before `/create-plan`** — the explore step catches assumptions and edge cases before you commit to an approach.
- **Commit plans before executing** — plans in `docs/plans/` with git timestamps are useful project history (and R&D evidence if applicable).
- **Let recipes accumulate** — `/save-recipe` and the auto-capture in `/execute` build a project-specific knowledge base over time.

## Examples

See `examples/` for minimal, realistic versions of:

- a seed-doc set (project brief + architecture)
- an execution plan
- a recipe
- an SR&ED log entry

They are intentionally small. The point is to show what "good enough" looks like so you can start with something real rather than a blank file.

## Contributing

Issues and PRs welcome. This template reflects one workflow — if you've found patterns that work well with Claude Code, share them.

## License

MIT — use it however you want.
