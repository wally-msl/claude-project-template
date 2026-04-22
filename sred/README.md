# SR&ED Documentation (Optional R&D Evidence Module)

This directory stores contemporaneous records of experimental development work. It was designed for Canadian [SR&ED (Scientific Research and Experimental Development)](https://www.canada.ca/en/revenue-agency/services/scientific-research-experimental-development-tax-incentive-program.html) tax credit claims, where "created as the work happens" records are the strongest form of evidence.

The pattern is useful beyond Canada. Any team that has had to reconstruct *why* a research direction was taken — months later, without the original reasoning — benefits from this kind of journal. If that doesn't describe you, delete this directory and skip the `/sred-log` command. The rest of the template doesn't depend on it.

See `../examples/sred/` for a sample hypothesis log with two dated entries.

## Why This Matters

The SR&ED program provides tax credits (up to 35% for CCPCs) for work that involves technological uncertainty — situations where it wasn't clear whether or how something could be achieved using available knowledge and technology.

The strongest evidence is *contemporaneous* — created as the work happens, not reconstructed months later for the claim. This directory, combined with git commit timestamps, provides that evidence trail.

## How It Works With This Template

1. **Define hypotheses** in your `CLAUDE.md` under the SR&ED section. These are the technological uncertainties you're investigating. Format: `H1: Can X achieve Y under constraint Z?`

2. **Log experiments** using the `/sred-log` command after completing experimental work. It creates structured entries with uncertainty, approach, observations, and next steps.

3. **Plans auto-tag** — when `/create-plan` creates a plan tagged with a hypothesis ID, it appends a pre-experiment entry documenting intent *before* execution.

4. **Execution auto-logs** — when `/execute` completes SR&ED-tagged work, it prompts for a post-experiment summary.

5. **Git commits are evidence** — descriptive commit messages with hypothesis IDs create a timestamped audit trail.

## File Organization

Create one file per hypothesis plus general files:

```
sred/
├── README.md                    # This file
├── h1-[hypothesis-slug].md      # Entries for hypothesis H1
├── h2-[hypothesis-slug].md      # Entries for hypothesis H2
├── infrastructure-setup.md      # Experimental environment construction
└── general-observations.md      # Cross-cutting findings
```

## Entry Format

```markdown
### [Date] — [Brief title]

**Uncertainty:** [What we didn't know]
**Approach:** [What we tried]
**Commits:** [git hashes]
**Observation:** [What happened]
**Next:** [What follows]
```

## Important Guidelines

- Write in factual, objective language — the CRA reviewer is the audience, not investors
- Don't overstate novelty — be honest about what's genuinely uncertain vs. routine engineering
- Document failures and dead ends — negative results are valid SR&ED evidence
- Record intent *before* experiments when possible (pre-logs are stronger evidence)
- Keep entries concise — a few sentences per field is sufficient

## Claim Preparation

For full SR&ED claim preparation (T661 forms, audit packages, filing), consider using structured SR&ED skills in Claude Cowork projects. These can analyze your documentation, conduct structured interviews, and generate CRA-ready filing packages.

Consult with an SR&ED-experienced accountant before filing. This documentation supports the claim but doesn't replace professional advice on eligibility and calculations.
