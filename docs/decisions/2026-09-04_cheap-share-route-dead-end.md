# ADR — Cheap-share route is a dead-end

- **Date:** 2026-09-04
- **Status:** Rejected (dead-end)
- **Parks:** vintages + time-opened fee cap ([2026-09-03](2026-09-03_vintage-pools-no-unit-price.md), [2026-09-03](2026-09-03_time-opened-fee-cap.md)) — parked for **complexity**, not rejected on the idle-pool / no-unit-`v` analysis.
- **Does not accept** a simpler option-2 design yet; that is the next pass.
- **Amends:** payout / wrapper comments in [2026-09-02](2026-09-02_tax-aware-contribution-credits.md) (still proposed). Confirms option 1 via labour-quota shares is not a way out.

## Context

The vintage design (annual budget `P_t`, default-in, no unit `v`, time-opened cap per lot) stopped wait-and-run and a day-one `k×` gold rush, but the lot / record-date / opening-factor machinery is hard to explain.

The alternative sketch: contribution points mint `p`; `p` is a cap on dividends over time **and** a quota of cheap €1 shares (1 share per 5,000 `p`, round up); year-end profit is split by shares; every €5,000 received (floor, carried) forces selling 1 share and burning 5,000 `p`.

Full note: [token-system-design/cheap-share-route.md](../../token-system-design/cheap-share-route.md).

## Decision

1. **Reject** the cheap-share route. Do not implement it. Do not use labour-quota €1 shares to dress a contribution reward as a dividend.
2. **Reject** burning `p` at a euro par (5,000 `p` per €5,000 received, or 1 `p` = €1 as a remaining-dividend cap). That is a unit price on the mint.
3. **Park** vintages and the time-opened fee cap. The no-unit-`v` / leftover-to-reserves / no-burn-for-taking-the-flow analysis still stands; the *packaging* is too heavy for now.
4. **Next pass:** option 2 (contingent invoiced fee, points as weights) with **reduced complexity**. Constraints that still bind: no euro par on `p`; no `v = pool / N`; do not mix dividend and fee on one instrument; governance share ≠ reward.

## Consequences

- A simpler story that fails characterisation is not an improvement on a correct-but-heavy option-2 vintage.
- Option 1 remains available only if allocation looks like **capital / membership**, not contribution points. Cheap extra shares whose number tracks points do not get there.
- Inbreng in nijverheid, done honestly, is a share-valuation event — often worse than a contingent fee — not a shelter.
- Next write-up should strip vintage machinery, not reintroduce a par or a share-quota.
