# ADR — Vintage pools instead of a unit certificate price

- **Date:** 2026-09-03
- **Status:** Proposed
- **Amends:** payout mechanics in [2026-09-02](2026-09-02_tax-aware-contribution-credits.md) (still proposed). Does not accept option 1 vs 2; it says how cash leaves **if** the instrument is a contingent fee.

## Context

The 2026-09-03 bonding-curve iteration dropped a mint-time euro rate `w = dc/dp`, which was correct. The fallback `v = pool / certificates outstanding` (leftover stays in the pot, burn on withdraw) still defines a **spot price on a growing stock**. Holders then wait until `v` is a “decent ROI”, the pot sits idle (nobody can spend or invest it), and they withdraw together. If that delay means the money is retained earnings, Refaqt pays VenB and the contributors’ BVs pay VenB again — whereas a same-year deductible fee would have been taxed once.

Capping the denominator (`v = pool / N_cap`) does not fix this. The GA then sets the price, either arbitrarily or to hit an ROI on contribution points, which is the grant-time pricing the tax analysis already rejected.

Full note: [token-system-design/vintage-pools.md](../../token-system-design/vintage-pools.md).

## Decision

Until counsel and an accountant say otherwise:

1. **Do not** use `v = pool / N_issued` or `v = pool / N_cap`, and **do not** choose `N_cap` or `v` to target an ROI on contribution points.
2. The GA/board sets each year’s **budget** `P_t` (waterfall + solvency + reserves), not a certificate price. Unallocated profit is Refaqt’s to invest.
3. Distribution is a **vintage**: default-in; invoice in the same fiscal year; leftover (opt-out, no invoice, over ceiling) goes to **operating reserves**, not back into a certificate pool.
4. Weights are **not burned** for taking a vintage. Retire only on a **fee ceiling** and/or **sunset**, or on exit.
5. Keep the mint `p = c0 · c^k` as a weight function. Do not quote €/certificate at mint or as a running withdrawal rate.
6. Same-year invoiced vintages are what make option 2 avoid double VenB. Vintages do not by themselves make a points-minted right into a dividend.

## Consequences

- Early-bird stays in the mint; waiting is no longer a second reward.
- Idle earmarked pots and coordinated runs go away if default-in and forfeiture are real.
- Refaqt invests retained profit that was never in `P_t`; contributors receive cash as vintages run.
- Ex-post returns still rise when Refaqt does well (`P_t` larger, ceiling hit sooner) without a GA-set ROI price.
- Round administration is heavier (default-in, deadlines, forfeiture).
- Option 1 (dividend on a share class) remains a separate characterisation fight; vintages do not win it.
- Next step: human review of same-year deduction, forfeiture, and ceiling vs sunset; then regulation text.
