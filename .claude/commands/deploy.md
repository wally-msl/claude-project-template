Deploy current changes to the server.

## Steps

1. **Stage and commit:**
   - `git add` all changed files
   - Write a descriptive commit message that explains what changed and why
   - Format: `[What changed]: [Why it was done]`

2. **Push to GitHub:**
   - `git push origin main` (or current branch)

3. **Deploy to server:**
   - Follow the deployment process defined in CLAUDE.md
   - If no deploy process is defined, ask me how to deploy

4. **Verify health:**
   - Check that services are running
   - If specific services were changed, check their logs
   - Run a basic smoke test if applicable

5. **Report status:**
   - List which services were restarted vs. kept running
   - Flag any warnings or errors in logs
   - Confirm the deployment is healthy

If any step fails, stop and report the error. Do not proceed past a failed step.
