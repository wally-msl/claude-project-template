# Project Brief: Ledger

**Version:** 0.1.0
**Date:** 2026-03-04

## What we're building

A small, single-tenant ledger service that records financial events for a handful of internal tools. Not a general-purpose accounting system — it tracks a fixed set of event types and exposes a read API for reporting.

## Why

Three internal tools currently each maintain their own running totals in ad-hoc tables. The numbers have disagreed twice in the past quarter, and reconciliation is manual. A single source of truth removes the disagreement and makes the reporting team's job possible.

## Non-goals

- Multi-tenant support. Explicitly single-tenant.
- UI. The service is API-only.
- Historical import from the legacy tables. We start clean at cutover.

## Constraints

- Must run on our existing Docker Compose host. No new infrastructure.
- Reporting team needs read access via a stable API by end of Q2.
- Write API only called by two internal services. Not exposed externally.

## Success looks like

- Both internal services writing to the ledger within two weeks of launch.
- Reporting team pulling from the ledger instead of the legacy tables.
- Zero reconciliation escalations for one full month post-cutover.

## Open questions

- Do we version events from day one, or add versioning when the first event shape changes?
- Does the reporting team need streaming reads, or is polling sufficient?
