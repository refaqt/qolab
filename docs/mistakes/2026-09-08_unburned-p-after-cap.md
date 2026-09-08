# 2026-09-08 — Unburned `p` after the cap is filled

## What happened

The option-2 sketch (and the parked vintage “do not burn for taking the flow” rule, read as never reducing `p`) left historical weights outstanding after the effort cap on that work was paid. Veterans and newcomers then contributing at the same point on the global bonding curve minted the same `Δp` for the same `Δc`, but veterans took far more of every later vintage.

## Why it went wrong

`p` is a claim on **this year’s** budget split. Once the opened cap on that work is exhausted, that claim has been used. Keeping the tokens turns already-paid weight into seniority on **new** work that takes the same risk at the same curve point. Early-bird belongs in the mint (`Δp` of earlier `Δc`), not in leftover stock after payout.

## Prevention rule

When remaining opened cap hits 0, `p` for that person (or lot) must be 0 **before** new work is minted. Amortize `p` by `alloc / rem` on each vintage; do not only clip invoices. Do not confuse that fraction with a euro par (`w`, `v = P/N`, 1 `p` = €1, `S − €`).

## Related

- [token-system-design/p-burn-remaining-cap.md](../../token-system-design/p-burn-remaining-cap.md)
- [docs/decisions/2026-09-08_p-burn-remaining-cap.md](../decisions/2026-09-08_p-burn-remaining-cap.md)
- [docs/mistakes/2026-09-03_unit-price-on-growing-pool.md](2026-09-03_unit-price-on-growing-pool.md)
- [docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md](2026-09-03_immediate-multiple-gold-rush.md)
