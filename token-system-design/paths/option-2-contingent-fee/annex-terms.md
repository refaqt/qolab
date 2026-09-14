# QOLAB annex — contract terms (checklist for counsel)

**Status: working checklist, not drafting.** Dutch wording of the *dienstenovereenkomst* (or IP licence) and the QOLAB annex is counsel’s. This page lists what the annex must say so that the [option-2 spec](README.md) and the [DVB filing](../../analysis/dvb-questions.md) describe the same facts. Two defaults chosen on 2026-09-14 are marked **(Proposed)** — [ADR 2026-09-14 defaults](../../../docs/decisions/2026-09-14_exit-death-and-disallowance-defaults.md). The cap is **one row per contributor** since [ADR 2026-09-14 one-row cap](../../../docs/decisions/2026-09-14_simplified-cap-one-row.md); clauses 8, 13, 14–16 and section F changed with it.

## A. Nature of the compensation

1. Compensation for accepted work is a **contingent success fee**, payable **only if** the CV opens a pool `P_t` under the regulation’s waterfall. No hourly invoice. No fixed fee.
2. `f` (documented effort: hours × the band frozen at accept, or a quoted effort) is a **ceiling** on cumulative invoices for that lot. It is not a fee earned, not a receivable, not “fees the contractor would normally have invoiced.” Hardware and equipment are not documented effort and do not enter `f`.
3. Nothing in the annex, a dashboard, or a statement may express remaining cap, remaining `p`, or `(k × E) / Δp` as euros owed or as a unit value of `p`.
4. `p` are dimensionless weights: contractually **not** parts or shares, never convertible into shares, non-transferable except to treasury, on death, or to a successor vehicle of the same beneficial owner.
5. The membership share (governance) is a separate instrument and does not set the payout.

## B. Pool and invoice mechanics

6. The waterfall for `P_t` is stated in the regulation (`min(policy % of profit or EBITDA, optional revenue cap, cash after reserves)`); the board **shall** open the pool when positive unless solvency forbids. `P_t` may be zero in any year.
7. Default-in allocation `alloc_i = min(P_t · p_i / Σ p, rem_i)`; invoice deadline in the same fiscal year as `P_t`; amounts VAT-exclusive; missed deadline → the slice forfeits to operating reserves, and `p` is haircut as if paid.
8. Cap rules, one row per contributor ([spec §5](README.md#5-cap-and-opening--one-row-per-contributor)): the ceiling is cumulative documented effort plus an opening, minus cumulative allocations, and never above `k` times cumulative documented effort. The opening for a year is `r` times the documented effort that was already on the books at the start of that year and is still not covered at its end. Work accepted in a year therefore opens nothing until it has survived one full allocation round unpaid, and the opening stops by itself once allocations reach documented effort, with the opened remainder still invoiceable. `k` and `r` are named as **policy parameters** set by the GA/board, described as a fee cap, never as a return, yield, or interest. The annex states the opening as a factor applied to unpaid documented work, never as a rate applied to a balance.
8b. **Where an investor leg exists**, the regulation states that `P_t` is **split first** between the contributor leg and the holder leg in the ratio of what each leg may still be paid, and only the contributor leg is divided by `p`. The split is **formulaic**: the board decides how much is distributed, and nobody votes on the division. Unabsorbed amounts re-pass within a leg only, never across legs; deviations are carried and corrected the following year. Mechanics: [capped-participating-bond §4](../capped-participating-bond/README.md); holder-side terms: [loan-regulations.md](../capped-participating-bond/loan-regulations.md).

9. The annex does not promise a multiple. It states that in years without a pool nothing is due and that a row may lapse without ever being invoiced. (This is what makes the ex-ante “expected value ≈ 1×” line filable if fallback B is ever used — see [spec §5](README.md#5-cap-and-opening--one-row-per-contributor).)

## C. Disallowance clause (Proposed: pool absorbs)

10. If the tax administration disallows part of a paid fee as exceeding professional needs (art. 53, 10° WIB 92), or otherwise denies a deduction while the fee remains a fee, the resulting tax at the CV (the add-back, its VenB, any tax increase and the art. 206/3 §1 effect on the offset of losses) is **borne by the CV** and funded from operating reserves and, if needed, the next `P_t`. There is **no clawback** from, and no credit note by, the contributor for the disallowed slice; their turnover and tax position are unchanged.
11. Rationale (record in the annex preamble or a side letter): only the excess is rejected and the administration bears the burden of proof; the contributor has already been taxed on the full amount; pushing the risk onto contributors would make the ceiling read as a loan-like receivable and would re-open the amount every time the CV is audited. The cost is borne pro rata by every holder through a smaller future `P_t`. Any reserve the CV keeps for it is treasury sized to the excess on open years, not a deductible provision ([2026-09-14 no-ruling log](../../../docs/log/2026-09-14_no-ruling-reserve-and-lookback.md)).
12. If instead the payment is **requalified** (hidden dividend with RV for which the CV is debtor; wage with RSZ), the annex allocates RV / RSZ per the statutory debtor and says whether the CV may pass RV on — a counsel item, not decided here.
13. If `k` or `r` is later reduced by counsel, a ruling condition, or an audit settlement, the reduction applies to **future opening**; cap already opened under the previous parameters is honoured (ask DVB explicitly in **(p)** whether a clawback would be expected). Because there is one row and no vintaging, such a change takes effect for every contributor in the same year; the annex says so plainly.

13b. **Uniform terms, amendable by majority, no individual veto.** The annex is one standard document; the only things that vary per contributor are hours and the frozen band. Contributors accept on signature that it may be amended by the general assembly on **one member, one vote**, and that they are bound by the outcome — no contributor holds a veto over a change that applies to everyone. The protection is clause 13: a reduction applies to **future opening** only, and cap already opened is honoured. The same pair of rules governs the [holder leg](../capped-participating-bond/loan-regulations.md) (clauses 15–17), so neither constituency can block a change the other accepts.

## D. Exit, death, succession (Proposed: continue as if present)

14. **Death** or transfer to a **successor vehicle** of the same beneficial owner: the row continues exactly as if the holder were present — opening while documented effort is still unrecovered, invoicing by the estate / successor — until the remaining ceiling is exhausted or a sunset, if any, hits.
15. **Voluntary exit** from the contractor relationship: the opening stops at the exit date (`r` becomes zero for that person); the opened remainder stays invoiceable without time limit; `p` burns as euros are taken.
16. **Exclusion** for cause (bad leaver): the row lapses to operating reserves at the exclusion date; `p` is retired. The grounds for exclusion are listed in the annex, not left to discretion.
17. The same three rules apply one level down for subpool euros of a sub-project. Leaving the CV as a **member** does not by itself change a row; only the contractor relationship does.
18. Tax treatment of a lapse (taxable disposal vs simply no invoice) is DVB **(r)**; the annex must not describe a lapse as a waiver of a receivable.

## D2. Contributor statement (Proposed)

24. A contributor may receive a statement of **their own row**, and only their own. It shows cumulative documented effort, unrecovered documented effort, the current ceiling, allocations to date, and **the number of past years in which the pool was zero**. It carries a standing line that the ceiling pays nothing unless the board opens a pool, and that the row may lapse unpaid.
25. The statement may show the tariff — what a fully unpaid year of documented work may be invoiced at after one, two, or five years, and the lifetime lid. It may **not** show a rate applied to a balance.
26. Never on a statement: any projection of a future ceiling, `rem / p`, any euros per `p`, any figure expressed per year or as a return, any total that includes opening that has not accrued yet, and the words *balance*, *saldo*, *tegoed*, *outstanding* or *owed* in any language.
27. The CV gives its accountant, and offers the contributor for theirs, a short written instruction that the ceiling is not a liability of the CV and not a receivable of the contributor, and that no provision or financial charge is recognised as the opening accrues. This is the clause that protects the characterisation in practice; the wording of the annex does not survive a contrary booking. **Note the contrast with the holder leg, and keep the two instructions apart:** a bond principal **is** a liability and is booked as one, while its uplift is **not** accrued until the board opens that leg ([loan-regulations clauses 22–23](../capped-participating-bond/loan-regulations.md)). Two opposite booking instructions cannot ride on one parameter name, which is a second reason `r_I` and `k_I` are named apart from `r` and `k`.

## E. Relationship and hygiene

19. Contractor is genuinely independent (own clients, no subordination); staff-like people are employees on euro payroll and receive no credits as wages in kind.
20. IP / CLA terms sit in the main contract; the annex only references them.
21. Sub-project entities: name the legal invoicing party (the CV, a BV, or the contributors on a disclosed split) — DVB **(o)**.
22. Evidence policy: keep the record of every year’s waterfall outcome (including `P_t = 0`), every lapsed lot, and every forfeited slice; these are the facts a filing relies on.
23. Sunset `T`, if adopted, is a lapse of **weights / lots**, never a share right (DVB **(g)**).

## F. Never in the annex

- A unit price, target ROI, “beats ETFs,” “will be worth more if you wait,” or a default multiple on a short payback.
- A promise that credits become shares, or a share count tied to hours, points, or `p`.
- Wording that books the ceiling as a liability of the CV or a receivable of the contributor. This is the one that decides the outcome in practice: once a bookkeeper puts the ceiling on a balance sheet, the opening becomes a financial charge to a related party and the tax analysis follows the books, whatever this annex says (clause 27).
- Any description of `r` as interest on a balance, or a ceiling written as a balance multiplied by `(1 + r)`.
- These words, in any language, anywhere in the annex or a statement: *interest, rente, intrest, yield, rendement, opbrengst, saldo, tegoed, schuldvordering, achterstal, outstanding, owed, balance, indexation*. Use *ceiling / plafond, opening, unrecovered documented effort, contingent success fee* instead. Those words are correct on the [holder leg](../capped-participating-bond/README.md), which really is debt — which is exactly why the two legs never appear in one document.
- `r_I`, `k_I`, the holder leg's terms, or any offering document material. The two instruments are never described by one parameter and never stated together ([2026-09-14 mistake](../../../docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md)).
