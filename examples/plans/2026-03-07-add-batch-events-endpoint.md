# Implementation Plan: Add batch events endpoint

**Overall Progress:** `0%`

## TLDR

Service A wants to post multiple events in a single request during its nightly reconciliation job. Add `POST /events/batch` that accepts an array of events and writes them in a single transaction. Rejects the whole batch on any validation failure.

## Critical Decisions

- **All-or-nothing transaction.** Partial success would create ambiguous state for callers. Reason: simpler failure semantics outweigh the retry cost.
- **Cap batch size at 500.** Protects the materialized view refresh from locking the table for too long under the current hardware. Revisit if service A needs more.
- **Reuse existing validation.** Same per-event validation as `POST /events`; no new rules.

## Tasks

- [ ] 🟥 **Step 1: Add handler and route** [component: api]
  - [ ] 🟥 Create `POST /events/batch` handler in `src/routes/events.ts`
  - [ ] 🟥 Input schema: array of existing event schema, length 1–500
  - [ ] 🟥 Return 201 with inserted ids on success, 400 with per-index errors on failure

- [ ] 🟥 **Step 2: Transactional insert** [component: db]
  - [ ] 🟥 Wrap insert in `BEGIN ... COMMIT` using existing pg pool helper
  - [ ] 🟥 Refresh balances materialized view once, after the batch commits
  - [ ] 🟥 Verify no partial writes on validation failure (integration test)

- [ ] 🟥 **Step 3: Tests** [component: api]
  - [ ] 🟥 Unit tests for input validation (size, shape)
  - [ ] 🟥 Integration test: 100-event batch succeeds end-to-end
  - [ ] 🟥 Integration test: one invalid event rejects the whole batch

- [ ] 🟥 **Step 4: Docs** [component: docs]
  - [ ] 🟥 Update `docs/architecture.md` — add batch endpoint to Write API section
  - [ ] 🟥 Update OpenAPI spec at `docs/api.yaml`

## Deploy Checklist

- [ ] Commit with descriptive message
- [ ] Push to GitHub
- [ ] Merge to main, run manual deploy (SSH + docker compose pull/up)
- [ ] Verify `/healthz` green
- [ ] Spot-check a 2-event batch against staging before service A cutover
