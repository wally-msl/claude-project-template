Document the current work for SR&ED (Scientific Research and Experimental Development) tax credit purposes.

## Context

This project's development work may qualify for Canadian SR&ED tax credits. Contemporaneous documentation — records created as the work happens, not reconstructed afterward — is the strongest form of evidence. Git commit timestamps provide the chronological proof; this command creates the narrative.

## What To Document

For the work we just completed or are currently doing:

1. **What was the technological uncertainty?**
   - What didn't we know how to do, or what wasn't sure to work?
   - Frame as a question: "Can X achieve Y under constraint Z?"
   - Link to hypothesis if applicable (check CLAUDE.md for hypothesis IDs)

2. **What did we try?**
   - Describe the approach taken
   - Reference specific git commits by hash
   - Note any alternative approaches considered and why they were rejected

3. **What did we observe?**
   - Did it work? Partially? Not at all?
   - What surprised us?
   - What did we learn that we didn't know before?

4. **What's next?**
   - If it worked: what's the next experiment?
   - If it didn't: what will we try differently?

## Output

Write a dated entry to the appropriate file in `sred/`. Create files organized by hypothesis or topic area — for example:

- `sred/h1-[hypothesis-slug].md`
- `sred/h2-[hypothesis-slug].md`
- `sred/infrastructure-setup.md` — Experimental environment construction
- `sred/general-observations.md` — Cross-cutting findings

## Format

### [Date] — [Brief title]

**Uncertainty:** [What we didn't know]
**Approach:** [What we tried]
**Commits:** [git hashes]
**Observation:** [What happened]
**Next:** [What follows]

## Important

- Write in factual, objective language — not promotional
- Don't overstate the novelty — be honest about what's genuinely uncertain vs. routine engineering
- The accountant and CRA reviewer are the audience, not investors
- Create the sred/ directory and files if they don't exist yet
