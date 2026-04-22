Perform a comprehensive code review of the recent changes. Be thorough but concise.

**Scope note:** this is an advisory prompt-driven checklist, not a scanner. It names the right categories but does not run `npm audit`, `gitleaks`, SAST, IaC policy, or the test suite. Treat the output as supplementary signal — for anything security-sensitive or production-bound, pair it with real tools in CI.

## Check For:

**Security**
- No API keys, passwords, or secrets in code (must be in env vars or secrets manager)
- No sensitive data logged or exposed in error messages
- Input validation on all external inputs
- Dependencies are from trusted sources

**Code Quality**
- No `any` types (TypeScript) or equivalent type-safety escapes
- Proper error handling for all async operations
- No hardcoded values that should be configurable
- No TODOs left unresolved
- No console.log left in production code — use proper logging
- Functions are focused and reasonably sized
- Names are clear and consistent

**Infrastructure** (if applicable)
- Docker: resource limits set, no unnecessary privilege escalation
- Network: services on correct networks, no unintended exposure
- Volumes: persistent data handled correctly
- Restart policies configured

**Tests** (if applicable)
- New functionality has test coverage
- Edge cases are covered
- Tests are deterministic (no flaky tests)

## Output Format

### ✅ Looks Good
- [Item 1]
- [Item 2]

### ⚠️ Issues Found
- **[Severity]** [File] - [Issue description]
  - Fix: [Suggested fix]

### 📊 Summary
- Files reviewed: X
- Critical issues: X
- Warnings: X

## Severity Levels
- **CRITICAL** - Security breach, data leak, credential exposure
- **HIGH** - Bugs, missing error handling, data integrity risks
- **MEDIUM** - Code quality, maintainability, performance concerns
- **LOW** - Style, minor improvements, documentation gaps
