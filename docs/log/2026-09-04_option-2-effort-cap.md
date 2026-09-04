# 2026-09-04 — Option-2 cap from documented effort

**Role(s):** finance, business-dev

## What happened

Next option-2 pass: keep minting weights with `p = c0 · c^k`; contractors invoice from a yearly pool `P_t` set by the GA; replace the parked per-lot `E_L` packaging with a simpler personal invoice ceiling.

First sketch used contribution points `c_ij`, `min(0, t-t_j)` (that term never grows), a **global** `k×` over all contributors, and `× €1` to get euros. Corrected: **per-person documented effort** `f_ij`, `max(0, t-t_j)`, subtract payouts, and **do not** treat the cap as the pool.

Working formula (`t` in years so `r` is a yearly parameter):

```
remaining_i = min(Σ_j f_ij · (1 + r · max(0, t − t_j)),  k · Σ_j f_ij) − Σ payouts_i
pay_i       = min(P_t · p_i / Σ p,  max(0, remaining_i))
```

`P_t` stays a solvency-checked GA/board budget. The cap only **clips** invoices. Leftover of `P_t` goes to operating reserves. No burn of `p`.

Two ledgers (aligned with [uniform points per hour](2026-09-04_points-per-hour-weight.md)):

| Ledger | What | Job |
| --- | --- | --- |
| Contribution points `c` | Same scoring for the same work (e.g. uniform points per hour — **not** industry rate) | Mint weights `p` |
| Documented effort `f_ij` | Hours × **frozen contractor band**, or a task estimate in the annex | Invoice ceiling |

A **band** is a rate-card line frozen at join / task accept (junior / senior / specialist €/h). Early-bird stays in `Δp`. Euro bounding stays in `f`. Do **not** mint from `f`: that reconstructs `w = df/dp` in €/`p`. Do not publish `remaining / p` or `(k × f) / Δp`. `× €1` on dimensionless points is a published par; if `c` is already euro-effort you have not escaped `E_L`, you have identified `c` with `f`.

`r` is a **cap-opening parameter**, not interest, not a yield. Do not book remaining cap as a receivable of the BV or a liability of the CV. Do not dashboard “€X still owed.” A ceiling is not consideration “to be received” (WBTW art. 26) while `P_t` may be zero — FPS still look at substance (DVB **(h)**), not the word “cap.”

Subtracting payouts is required. Calendar age of `f` still opens remaining **after** a short payback (about `r · Σ f` per year) unless **freeze after 1× paid**. That freeze is what kills the trailing coupon / gold rush and the interest-on-a-balance optics.

**Record date** is eligibility, not delayed logging: log points and `f_ij` when the work is accepted; work in fiscal year `Y` first sits in `P_{Y+1}`. Same-year work-and-invoice looks like this year’s wage.

Logging `f_ij` does **not** automatically trigger VAT/tax at that instant if `f` is a **reference amount for the contractual ceiling** (quoted effort / band × hours), the contract says there is **no** hourly invoice, and compensation is only a contingent success fee **if** a pool exists. Wording “fees he would normally have invoiced” sounds like an unissued invoice (VAT when the service was performed, art. 22 / 26). Rename `f` to documented effort / reference fee / quoted effort. Still a DVB hypothesis (**(i)** and **(h)**), not a ruling.

## Decisions

Proposed (not accepted): simpler option-2 cap on per-person `f_ij`; points ≠ `f`; `P_t` is not the cap; call `r` a parameter; do not describe or book the cap as a claim. Still bound by [ADR 2026-09-04 fee cap is not a unit price of `p`](../decisions/2026-09-04_fee-cap-not-unit-price.md) and [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md).

## Open Questions

- Freeze after 1× paid vs let `r` keep opening remaining (gold rush / receivable optics).
- DVB (h): opened cap vs interest / receivable.
- DVB (i): effort cap vs implied €/`p`; logging `f` vs VAT/tax at grant. Safe only if `f` is a contractual ceiling document, not a deferred invoice.
- Values of `k` and `r` (examples elsewhere use `k = 3`, `r = 0.20`).

## Next Steps

- Counsel + accountant on (h) and (i) and on the wording of `f` in the dienstenovereenkomst.
- If freeze is accepted, write the formula into the option-2 spec (and an ADR). Do not draft regulation around “would normally have invoiced.”
