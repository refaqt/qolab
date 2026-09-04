# 2026-09-04 — Cheap €1 shares as a labour-quota dividend

## What happened

After parking vintages as too complicated, the next sketch minted `p` from contribution points, used `p` as a euro cap on dividends **and** as a quota of cheap €1 shares, split profit by those shares, and burned 5,000 `p` (and one share) per €5,000 received.

## Why it went wrong

The €1 share does not do the economic work; `p` does. Share *count* still tracks labour, so option 1 (30% dividend, no VAT, no tax at grant) is a weaker characterisation than before, not a stronger one. Burning `p` at 5,000 per €5,000 is **1 `p` = €1** — a euro par on the mint, the same class of fact as the rejected U-token and `w = dc/dp`. The full euro cap is open on day one, so a forecasted fat year is a gold rush at ~1× points-as-euros. Burn-on-payout also makes holders want the GA to retain earnings until the jackpot year.

## Prevention rule

Do not issue extra profit-sharing shares whose number is set by contribution points, including at a €1 ticket price. Do not give `p` a euro par (cap, burn, or FX). Keep the governance share off the reward. A points-minted right is a fee story (option 2) or it will be recharacterised as one; dressing it as a dividend does not win option 1.

## Related

- [token-system-design/cheap-share-route.md](../../token-system-design/cheap-share-route.md)
- [docs/decisions/2026-09-04_cheap-share-route-dead-end.md](../decisions/2026-09-04_cheap-share-route-dead-end.md)
- [docs/mistakes/2026-09-03_unit-price-on-growing-pool.md](2026-09-03_unit-price-on-growing-pool.md)
- [docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md](2026-09-03_immediate-multiple-gold-rush.md)
