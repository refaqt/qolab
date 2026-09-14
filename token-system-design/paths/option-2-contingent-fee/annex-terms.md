# QOLAB annex — contract terms (checklist for counsel)

**Status: working checklist, not drafting.** Dutch wording of the *dienstenovereenkomst* (or IP licence) and the QOLAB annex is counsel’s. This page lists what the annex must say so that the [option-2 spec](README.md) and the [DVB filing](../../analysis/dvb-questions.md) describe the same facts. Two defaults chosen on 2026-09-14 are marked **(Proposed)** — [ADR 2026-09-14 defaults](../../../docs/decisions/2026-09-14_exit-death-and-disallowance-defaults.md).

## A. Nature of the compensation

1. Compensation for accepted work is a **contingent success fee**, payable **only if** the CV opens a pool `P_t` under the regulation’s waterfall. No hourly invoice. No fixed fee.
2. `f` (documented effort: hours × the band frozen at accept, or a quoted effort) is a **ceiling** on cumulative invoices for that lot. It is not a fee earned, not a receivable, not “fees the contractor would normally have invoiced.”
3. Nothing in the annex, a dashboard, or a statement may express remaining cap, remaining `p`, or `(k × E) / Δp` as euros owed or as a unit value of `p`.
4. `p` are dimensionless weights: contractually **not** parts or shares, never convertible into shares, non-transferable except to treasury, on death, or to a successor vehicle of the same beneficial owner.
5. The membership share (governance) is a separate instrument and does not set the payout.

## B. Pool and invoice mechanics

6. The waterfall for `P_t` is stated in the regulation (`min(policy % of profit or EBITDA, optional revenue cap, cash after reserves)`); the board **shall** open the pool when positive unless solvency forbids. `P_t` may be zero in any year.
7. Default-in allocation `alloc_i = min(P_t · p_i / Σ p, rem_i)`; invoice deadline in the same fiscal year as `P_t`; amounts VAT-exclusive; missed deadline → the slice forfeits to operating reserves, and `p` is haircut as if paid.
8. Lot rules: 1× for the first 12 unpaid months; opening only while `paid < E`; freeze when `paid ≥ E` with the opened remainder still invoiceable; oldest unpaid lot first. `k` and `r` are named as **policy parameters** set by the GA/board, described as a fee cap, never as a return, yield, or interest.
9. The annex does not promise a multiple. It states that in years without a pool nothing is owed and that lots may lapse unpaid. (This is what makes the ex-ante “expected value ≈ 1×” line filable if fallback B is ever used — see [spec §5](README.md#5-cap-and-opening).)

## C. Disallowance clause (Proposed: pool absorbs)

10. If the tax administration disallows part of a paid fee as exceeding professional needs (art. 53, 10° WIB 92), or otherwise denies a deduction while the fee remains a fee, the resulting tax at the CV (the add-back, its VenB, any tax increase and the art. 206/3 §1 effect on the offset of losses) is **borne by the CV** and funded from operating reserves and, if needed, the next `P_t`. There is **no clawback** from, and no credit note by, the contributor for the disallowed slice; their turnover and tax position are unchanged.
11. Rationale (record in the annex preamble or a side letter): only the excess is rejected and the administration bears the burden of proof; the contributor has already been taxed on the full amount; pushing the risk onto contributors would make the ceiling read as a loan-like receivable and would re-open the amount every time the CV is audited. The cost is borne pro rata by every holder through a smaller future `P_t`. Any reserve the CV keeps for it is treasury sized to the excess on open years, not a deductible provision ([2026-09-14 no-ruling log](../../../docs/log/2026-09-14_no-ruling-reserve-and-lookback.md)).
12. If instead the payment is **requalified** (hidden dividend with RV for which the CV is debtor; wage with RSZ), the annex allocates RV / RSZ per the statutory debtor and says whether the CV may pass RV on — a counsel item, not decided here.
13. If `k` is later reduced by counsel, a ruling condition, or an audit settlement, the reduction applies to **future opening**; cap already opened under the previous `k` is honoured (ask DVB explicitly in **(p)** whether a clawback would be expected).

## D. Exit, death, succession (Proposed: continue as if present)

14. **Death** or transfer to a **successor vehicle** of the same beneficial owner: the lot continues exactly as if the holder were present — opening while unpaid, invoicing by the estate / successor — until its cap is exhausted or a sunset, if any, hits.
15. **Voluntary exit** from the contractor relationship: opening freezes at the exit date; the opened remainder stays invoiceable without time limit; `p` burns as euros are taken.
16. **Exclusion** for cause (bad leaver): the lot lapses to operating reserves at the exclusion date; `p` is retired. The grounds for exclusion are listed in the annex, not left to discretion.
17. The same three rules apply one level down for subpool euros of a sub-project. Leaving the CV as a **member** does not by itself change a lot; only the contractor relationship does.
18. Tax treatment of a lapse (taxable disposal vs simply no invoice) is DVB **(r)**; the annex must not describe a lapse as a waiver of a receivable.

## E. Relationship and hygiene

19. Contractor is genuinely independent (own clients, no subordination); staff-like people are employees on euro payroll and receive no credits as wages in kind.
20. IP / CLA terms sit in the main contract; the annex only references them.
21. Sub-project entities: name the legal invoicing party (the CV, a BV, or the contributors on a disclosed split) — DVB **(o)**.
22. Evidence policy: keep the record of every year’s waterfall outcome (including `P_t = 0`), every lapsed lot, and every forfeited slice; these are the facts a filing relies on.
23. Sunset `T`, if adopted, is a lapse of **weights / lots**, never a share right (DVB **(g)**).

## F. Never in the annex

- A unit price, target ROI, “beats ETFs,” “will be worth more if you wait,” or a default multiple on a short payback.
- A promise that credits become shares, or a share count tied to hours, points, or `p`.
- Wording that books the ceiling as a liability of the CV or a receivable of the contributor.
- Any description of `r` as interest on a balance.
