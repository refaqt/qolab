# 2026-09-04 — Cheap €1 shares as a labour-quota dividend

## What happened

After parking vintages as too complicated, the next sketch minted `p` from contribution points, used `p` as a euro cap on dividends **and** as a quota of cheap €1 shares, split profit by those shares, and burned 5,000 `p` (and one share) per €5,000 received.

## Why it went wrong

The €1 share does not do the economic work; `p` does. Share *count* still tracks labour, so option 1 (30% dividend, no VAT, no tax at grant) is a weaker characterisation than before, not a stronger one. Burning `p` at 5,000 per €5,000 is **1 `p` = €1** — a euro par on the mint, the same class of fact as the rejected U-token and `w = dc/dp`. The full euro cap is open on day one, so a forecasted fat year is a gold rush at ~1× points-as-euros. Burn-on-payout also makes holders want the GA to retain earnings until the jackpot year.

## Prevention rule

Do not issue extra profit-sharing shares whose number is set by contribution points, including at a €1 ticket price, at €0.10 vs €10 investor shares, **when there are no investors yet**, as an **informal** or **MoU** “we’ll put it on paper later” ledger, or as **unpaid / “given”** paper that is meant to look like startup founder stock. Do not set the issue prices of a contributor class and an investor class so that a published quota converts hours into euros of capital (€1 / €100 with `p = c/1000` states €10 of capital per hour). Do not try to rescue the quota with a **sunset** of the profit right: it bounds duration, not amount, it reads as deferred pay for the work that minted it, and it makes the grant easier to value. Do not give `p` a euro par (cap, burn, or conversion rate). Keep the governance share off the reward. A points-minted right is a fee story (option 2) or it will be recharacterised as one; dressing it as a dividend does not win option 1.

## Related

- [token-system-design/cheap-share-route.md](../../token-system-design/cheap-share-route.md)
- [docs/decisions/2026-09-04_cheap-share-route-dead-end.md](../decisions/2026-09-04_cheap-share-route-dead-end.md)
- [docs/mistakes/2026-09-03_unit-price-on-growing-pool.md](2026-09-03_unit-price-on-growing-pool.md)
- [docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md](2026-09-03_immediate-multiple-gold-rush.md)
- [docs/log/2026-09-08_option-1-tenth-vs-ten-euro-shares.md](../log/2026-09-08_option-1-tenth-vs-ten-euro-shares.md) (same class of fact at €0.10 vs €10, no burn)
- [docs/log/2026-09-10_no-investors-euro-shares.md](../log/2026-09-10_no-investors-euro-shares.md) (same quota with no investors; informal mapping is still a quota)
- [docs/log/2026-09-10_startup-equity-mou.md](../log/2026-09-10_startup-equity-mou.md) (unpaid / given / revalued / MoU class still a quota if `N = f(work)`)
- [docs/log/2026-09-11_cheap-share-ab-classes-sunset.md](../log/2026-09-11_cheap-share-ab-classes-sunset.md) (linear quota, €1 / €100 classes, 10-year sunset — same rejection; the price pair publishes €/hour)
- [docs/mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md](2026-09-10_inbreng-in-nijverheid-plan-ahead.md) (honest nijverheid still needs a plan-ahead commitment)
