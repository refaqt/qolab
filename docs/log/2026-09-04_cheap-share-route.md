# 2026-09-04 — Cheap-share route (dead-end)

**Role(s):** finance, business-dev

## What happened

Parked vintages: the time-opened fee cap per lot is too complicated to explain. Investigated a simpler-looking option-1 sketch — contribution points mint `p`; `p` caps dividends over time and sets how many €1 shares a contributor may buy (1 per 5,000 `p`, round up); profit is split by shares; every €5,000 received (floor, carried) forces selling one share and burning 5,000 `p`. Worked the Alex / Bill year-1 example (€10,000 profit → 11 vs 8 shares). Wrote [token-system-design/cheap-share-route.md](../../token-system-design/cheap-share-route.md). Rejected the route: [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md). Logged the failed approach in [docs/mistakes/2026-09-04_cheap-share-euro-par.md](../mistakes/2026-09-04_cheap-share-euro-par.md).

## Decisions

Rejected (dead-end): cheap extra shares as the reward; 1 `p` = €1 as cap or burn FX; labour-quota shares as a path to 30% dividend treatment. Parked (complexity, not merits): vintage `P_t` + time-opened lots. Next pass is option 2 with less machinery. Constraints that still bind: no euro par on `p`; no unit `v`; do not mix dividend and fee on one instrument; governance share ≠ reward.

## Open Questions

- How little option-2 machinery is enough: weights + a board-set budget + a 1× (or documented-effort) cap, without lots that open over time?
- Whether a record date / one-year delay is still needed if the lifetime multiple is not open on day one.
- DVB still required before anyone is promised a credit; characterisation of cash-out as fee remains the live question.

## Next Steps

- Iterate option 2 with reduced complexity (not this cheap-share wrapper, not full vintage lots).
- Counsel + accountant after that simpler spec exists.
