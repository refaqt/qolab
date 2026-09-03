# 2026-09-03 — Unit price on a growing certificate pool

## What happened

After dropping the mint-time rate `w = dc/dp`, the working recommendation became `v = pool / certificates outstanding`, with leftover left in the pot and burn on withdraw. A variant `v = pool / (capped N)` was the other way to get a “decent” unit price.

## Why it went wrong

A unit price on a **stock** that grows, with burn-on-withdraw and no lapse, is a free option on pool growth. Holders wait; then they all exercise. The earmarked pot sits idle (cannot be invested). Same-year deduction of a success fee never happens, so profit can be taxed at Refaqt and again at the contributors’ BVs. Capping `N` only moves the price into the GA, and calibrating that cap to an ROI **is** a euro price on contribution points.

## Prevention rule

Do not give contribution certificates a euro spot price, including payout-time `v = pool / N`. Split **this year’s** budget across weights (default-in). Do not burn for taking a vintage. Do not recycle leftover into the certificate pot. Do not choose a denominator or a rate to hit a target ROI on points.

## Related

- [token-system-design/vintage-pools.md](../../token-system-design/vintage-pools.md)
- [docs/decisions/2026-09-03_vintage-pools-no-unit-price.md](../decisions/2026-09-03_vintage-pools-no-unit-price.md)
