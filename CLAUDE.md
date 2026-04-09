# [Project Name] — Claude Code Project Instructions

## Project Overview

<!-- [PLACEHOLDER] Describe what you're building in 2-3 sentences. What is this project?
     What problem does it solve? This gives Claude Code the big picture. -->

[Describe your project here.]

## Who I Am

<!-- [PLACEHOLDER] Describe your technical level and how you want Claude to work with you.
     Are you a senior engineer who wants terse output? A technical founder who needs
     inline explanations? Adjust the instructions below to match. -->

I'm the [role — e.g., sole developer, technical founder, lead engineer]. I'm [describe your technical level — e.g., "a senior engineer comfortable with distributed systems" or "technically literate but not a daily coder"]. Be a thinking partner: push back on weak reasoning, explain technical terms inline on first use, and produce concrete artifacts.

## Tech Stack

<!-- [PLACEHOLDER] List your actual technologies. Claude Code uses this to write
     appropriate code and make informed suggestions. -->

- **Language:** [e.g., TypeScript, Python, Go]
- **Framework:** [e.g., Next.js, FastAPI, Express]
- **Database:** [e.g., PostgreSQL, MongoDB, SQLite]
- **Infrastructure:** [e.g., Docker Compose on VPS, Kubernetes, Vercel]
- **Monitoring:** [e.g., Prometheus + Grafana, Datadog, none yet]
- **Secrets:** [e.g., SOPS + age, Vault, .env files]
- **CI/CD:** [e.g., GitHub Actions, manual deploy]

## Key Architecture Decisions

<!-- [PLACEHOLDER] List the 3-5 most important design decisions in your project.
     These are things Claude should respect and not casually suggest changing.
     Delete the examples and add your own. -->

- **[Decision 1]:** [What you chose and why. e.g., "Monolith first. We're pre-launch and a monolith is simpler to deploy and debug. Microservices when we have a reason."]
- **[Decision 2]:** [What you chose and why.]
- **[Decision 3]:** [What you chose and why.]

## Development Workflow

<!-- [PLACEHOLDER] Describe how code gets from your editor to production.
     Claude Code can handle multi-step workflows if you describe them clearly. -->

1. Edit files locally in this repo
2. Commit and push to GitHub
3. [Describe your deploy process — e.g., "SSH into server, pull, restart services"]

<!-- If Claude Code should handle the full deploy cycle, describe it explicitly:
     "When I say 'deploy,' that means: git add, commit with a descriptive message,
     push, SSH into user@server, cd /path/to/project, git pull, ./deploy.sh" -->

### Session Start

<!-- Optional but recommended: give Claude Code a way to orient itself at the
     start of each session. -->

At the start of every new session, run `git log --oneline -10` to review recent changes. This seeds your context with what's been worked on recently.

## Deployment Details

<!-- [PLACEHOLDER] Fill in your actual deployment targets. Delete what doesn't apply. -->

- **Server SSH:** `ssh [user]@[hostname]`
- **Repo path on server:** `[/path/to/project/]`
- **Deploy script:** `[./deploy.sh or describe manual steps]`
- **Notes:** [Any quirks — e.g., "non-interactive SSH doesn't load shell profile, prefix commands with `export PATH=/usr/local/bin:$PATH`"]

## Git Practices

- Commit messages should be descriptive: `[What changed]: [Why it was done]`
  - Good: `Add rate limiting middleware: prevent API abuse before launch`
  - Good: `Fix Redis connection timeout: was using default 5s, production needs 30s`
  - Bad: `fix stuff`, `update files`, `misc changes`
- Commit directly to main for most changes. Use branches for risky or multi-day work.
- Tag milestones: `git tag -a v0.1.0 -m "Description of milestone"`

<!-- If you use SR&ED: "Commit messages serve as SR&ED evidence.
     Include hypothesis IDs when relevant." -->

## Document Conventions

Canonical documents live in `docs/`. When updating any document in `docs/`:

- Increment the version number following semantic versioning (MAJOR.MINOR.PATCH)
- Update the date
- Add a changelog entry describing what changed
- MAJOR: architectural changes, new systems, fundamental approach changes
- MINOR: new sections, significant additions, revised workflows
- PATCH: corrections, clarifications, minor updates

<!-- [PLACEHOLDER] List your canonical documents once they exist. Example:
     - docs/architecture.md — technical architecture
     - docs/onboarding.md — setup guide
     When renaming a versioned file, update all references. -->

Current canonical documents:
- [List your docs here as you create them]

## Code Style

<!-- [PLACEHOLDER] Define your conventions. Delete what doesn't apply, add your own. -->

- [Language] for [component]
- Markdown for documentation
- YAML for configuration
- One command per code block when giving terminal instructions
- Minimal, modular code — no over-engineering
- [Add your testing philosophy — e.g., "Red/green TDD for all services" or "Tests for critical paths, skip trivial ones"]

## What I Don't Want

<!-- Adjust this list to match your preferences. These are instructions to Claude Code
     about what to avoid. -->

- Filler praise or restating my questions
- Enterprise-grade solutions when scrappy-but-functional works
- Defaulting to the most complex approach
- Generic commit messages
- [Add your own — e.g., "Changes that break backwards compatibility without discussion"]

## SR&ED Documentation (Optional)

<!-- Delete this section if you're not doing SR&ED.
     If you are, define your experimental hypotheses here. -->

Work in this repo may qualify for Canadian SR&ED tax credits. When making changes related to experimental hypotheses, note the connection in commit messages and update files in the `sred/` directory. Key hypotheses:

- H1: [Define your first hypothesis — what technological uncertainty are you investigating?]
- H2: [Second hypothesis]
- H3: [Third hypothesis]

<!-- See sred/README.md for detailed SR&ED documentation setup. -->
