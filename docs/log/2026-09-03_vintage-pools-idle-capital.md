# 2026-09-03 — Vintage pools vs idle capital and double VenB

**Role(s):** finance, business-dev

## What happened

The `v = pool / certificates issued` fallback (and `v = pool / capped N`) was checked against withdrawal incentives. Both create a unit price on a growing stock: people wait for a decent ROI, then withdraw together; the pot cannot be invested; delayed option-2 payouts let Refaqt VenB and BV VenB stack. Wrote [token-system-design/vintage-pools.md](../../token-system-design/vintage-pools.md) and proposed [ADR 2026-09-03](../decisions/2026-09-03_vintage-pools-no-unit-price.md). Logged the failed approach in [docs/mistakes/2026-09-03_unit-price-on-growing-pool.md](../mistakes/2026-09-03_unit-price-on-growing-pool.md).

## Decisions

Proposed (not accepted): no unit `v`; each year a vintage budget `P_t`; default-in; leftover to reserves; no burn for taking a vintage; ceiling and/or sunset; keep the mint curve as weights only. Double VenB is avoided only if the vintage is a same-year deductible fee (option 2).

## Open Questions

- Ceiling (`k × effort`) vs sunset (`T` vintages) if a reference rate feels like pricing points — refined in [ADR 2026-09-03 time-opened fee cap](../decisions/2026-09-03_time-opened-fee-cap.md); `(k × E) / Δp` is not a unit price of `p` ([ADR 2026-09-04](../decisions/2026-09-04_fee-cap-not-unit-price.md)).
- Accountant: can a default-in vintage be provisioned so VenB matches the fee year.
- DVB items (e)–(h) in the vintage-pools note.

## Next Steps

- Counsel + accountant on vintages, forfeiture, opened cap vs interest, and option 2 matching.
- Then draft the QOLAB regulation around vintages and the time-opened cap, not around a withdrawal rate.
