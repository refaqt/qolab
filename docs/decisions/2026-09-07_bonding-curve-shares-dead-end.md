# ADR — Bonding-curve shares with cheap grant value is a dead-end

- **Date:** 2026-09-07
- **Status:** Rejected (dead-end)
- **Does not accept** option 2 yet; that remains the next pass.
- **Does not revive** cheap-share ([2026-09-04](2026-09-04_cheap-share-route-dead-end.md)).
- **Amends:** payout / wrapper comments in [2026-09-02](2026-09-02_tax-aware-contribution-credits.md) (still proposed). Confirms option 1 via labour-quota shares on a steep bonding curve is not a way out.

## Context

Cheap extra shares were already rejected as a dividend wrapper: share count still tracks labour, and a euro par on `p` prices the mint. A follow-up sketch tried to keep grant-time contribution value **constant and low** (€0.01 per point) and still pay a return by minting **shares** on `p = c0 · c^k` with a very small `k`, and by letting **revenues mint on the same curve** so price rises quickly.

Spreadsheet: [token-system-design/2026-09-07_token-system-calculation.ods](../../token-system-design/2026-09-07_token-system-calculation.ods). Session note: [docs/log/2026-09-07_bonding-curve-shares-dead-end.md](../log/2026-09-07_bonding-curve-shares-dead-end.md).

The curve that makes price rise fast mints almost all shares at the origin. Later contributions get a very low number of shares. The multiple needed to climb out of the cheap grant value is extreme and unpractical for anyone but the first mover.

## Decision

1. **Reject** steep bonding-curve shares with a cheap constant contribution value, including when revenues mint on that curve. Do not implement it.
2. **Do not** treat this as a fix for cheap-share. It still uses labour-quota shares as the reward and publishes a euro price per share.
3. **Next pass:** option 2 (contingent invoiced fee, points as weights) with **reduced complexity**. Constraints that still bind: no euro par on `p`; no `v = pool / N`; an effort-tied fee cap is **not** a unit price of `p` ([ADR 2026-09-04](2026-09-04_fee-cap-not-unit-price.md)); do not mix dividend and fee on one instrument; governance share ≠ reward.

## Consequences

- Low grant-time value, a fast price rise, and a usable later mint cannot be had together on one power-law share curve.
- Option 1 remains available only if allocation looks like **capital / membership**, not contribution points routed through a bonding curve.
- Next write-up should stay on simpler option 2, not another share-curve wrapper.
