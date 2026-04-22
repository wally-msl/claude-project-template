# Technical Architecture: Ledger

**Version:** 0.1.0
**Date:** 2026-03-04

## Stack

- **Language:** TypeScript (Node 20)
- **Framework:** Fastify
- **Database:** PostgreSQL 16
- **Infrastructure:** Docker Compose on the existing VPS
- **Secrets:** SOPS + age (matches current convention)
- **CI/CD:** GitHub Actions — tests on PR, manual deploy on merge to main

## Shape

Single service, two surfaces:

1. **Write API** — internal-only. Two endpoints: `POST /events` and `POST /events/batch`. Callers are service A and service B.
2. **Read API** — internal-only. Query endpoints for the reporting team. Pagination required; streaming deferred.

Storage is a single append-only `events` table with a strict schema and a secondary `balances` materialized view refreshed on write.

## Key decisions

- **Append-only events, not mutable rows.** Every financial change is an event; nothing is edited in place. Reversals are compensating events. Reason: audit trail and reproducibility.
- **Materialized view for balances.** Avoids recomputing sums on every read. Refreshed synchronously on write — volume is low enough that this is fine.
- **No message queue.** Direct HTTP calls from service A and service B. Queues would be over-engineered for two known callers.
- **Single-tenant by design.** No tenant ID on any row. Adding one later would be a migration — accepted.

## Deployment

- Build image in CI, push to GHCR.
- SSH to the VPS, `docker compose pull ledger && docker compose up -d ledger`.
- Health check: `/healthz` on port 8080.

## Data model (current)

```
events(
  id           uuid primary key,
  event_type   text not null,
  amount       numeric(18,4) not null,
  currency     text not null,
  occurred_at  timestamptz not null,
  recorded_at  timestamptz not null default now(),
  source       text not null,
  metadata     jsonb not null default '{}'::jsonb
)
```

Event types are validated against an enum-like allowlist in code, not in the database. Keeps migrations lightweight.

## Out of scope (v1)

- Event versioning (add when first schema change needed)
- Streaming reads
- External API exposure
- Multi-currency conversion (events store currency but we don't convert)
