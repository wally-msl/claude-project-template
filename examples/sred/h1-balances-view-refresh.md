# H1: Materialized view refresh under write load

**Hypothesis:** Can a synchronously-refreshed materialized view for balances sustain the expected write rate from service A's nightly reconciliation (peak ~300 events/minute over ~20 minutes) without blocking the write path beyond 200ms per event?

This was not obvious from available documentation. Postgres `REFRESH MATERIALIZED VIEW` takes an exclusive lock, and we could not find benchmarks at our row counts and hardware profile.

---

### 2026-03-12 — Baseline measurement

**Uncertainty:** Unknown whether synchronous refresh on every write would exceed the 200ms budget at realistic batch sizes.

**Approach:** Instrumented the write path with timing around the refresh call. Ran a 10,000-event load test against staging, bucketed by batch size (1, 10, 50, 100, 500).

**Commits:** `a3f2c11`, `b7d8e04`

**Observation:** Refresh time grew roughly linearly with the base table size, not with batch size. At 1.2M rows (current staging), refresh averaged 340ms — above budget. Batch size had almost no effect, which was counter to our initial assumption.

**Next:** Test `REFRESH MATERIALIZED VIEW CONCURRENTLY`, which requires a unique index on the view but allows reads during refresh. Open question: does it also reduce write-path latency or just read-path latency?

---

### 2026-03-14 — Concurrent refresh test

**Uncertainty:** Whether `CONCURRENTLY` reduces the blocking window for writers, or only for readers.

**Approach:** Added unique index to the balances view. Re-ran the 10,000-event test with concurrent refresh enabled. Measured both write-path latency and read-path latency during refresh.

**Commits:** `c0a1f20`, `d5b2e88`

**Observation:** `CONCURRENTLY` reduced read-path blocking to near zero as expected, but write-path latency was slightly *higher* (avg 380ms) — concurrent refresh is more work overall. This confirmed that synchronous refresh on every write is not viable at our target row counts.

**Next:** Move to asynchronous refresh — trigger-based queue of pending refreshes, drained by a background worker. Accept eventual consistency on balances (seconds, not milliseconds) as a design tradeoff. Will document this decision in `docs/architecture.md`.
