# Loan Regulations — terms checklist for counsel

**Status: working checklist, not drafting.** Dutch wording of the issue conditions and the Loan Regulations (*leningsreglement*) is counsel's. This page lists what the Regulations must say so that the [path note](README.md), the [option-2 annex](../option-2-contingent-fee/annex-terms.md) and the [DVB filing](../../analysis/dvb-questions.md) describe the same facts. Nothing here is accepted; the path is **open (proposed)** — [ADR 2026-09-14 investor leg](../../../docs/decisions/2026-09-14_investor-leg-capped-participating-bond.md).

Numbering continues the option-2 annex where a clause is the mirror of one there, so the two documents can be read side by side.

## A. Nature of the instrument

1. The instrument is a **subordinated, profit-participating bond**. It is not a share, not a membership right, and carries no vote in the general assembly.
2. It is **subordinated** to all other creditors of the CV, has **no fixed maturity** (or a maturity subject to the solvency test), and both principal and uplift are payable **only** out of `P^I_t` under the waterfall in the regulation. The holder may never be repaid.
3. Positions are **non-transferable** except to a successor vehicle of the same beneficial owner or on death. No peer market, no secondary trading, off-chain register.
4. **Nothing is issued for work.** Subscription is in **cash only**. The amount a person may advance is not a function of hours, `c`, `p`, or the contribution ledger, and no document, side ledger, or practice links the two.
5. Holders receive **contractual information rights**, not governance rights.

## B. The row

6. For each position the Regulations state, in this order and in these words: the principal still outstanding; an uplift accruing at `r_I` per year on the principal that was outstanding **at the start of the year**; the fact that a payment reduces outstanding principal and accrued uplift **in the same proportion**; and a **lifetime lid** of `k_I` times everything advanced.
7. The lid is stated as a bound on the **total ever paid** on the instrument, principal included. The Regulations do **not** state it as a target, a projection, or an expected outcome.
8. Money advanced during a year accrues nothing in that year.
9. `r_I` and `k_I` are named as **policy parameters** set by the general assembly, described as a cap on a contingent return. They are **not** the option-2 parameters `r` and `k` and are never described as the same parameter (see §F).
10. A **de-minimis close-out threshold** is stated: below it the position is paid in full and closed, rather than amortising asymptotically.
11. The Regulations state plainly that in years without a pool nothing is paid, and that a position may be closed having returned less than the principal advanced.

## C. The split

12. The regulation states the two-leg waterfall: `P_t` is computed first, then split between the contributor leg and the holder leg in the ratio of the two legs' remaining amounts, then allocated inside each leg. The split is **formulaic**; the board decides how much is distributed, not how it is divided.
13. Unabsorbed amounts are re-passed **within a leg only**, never across legs, and anything neither leg absorbs returns to reserves and the mission. Deviations from the ratio are carried and corrected in the following year.
14. The yearly order of operations is stated explicitly ([path note §4.1](README.md)), so that a reader can reproduce a year's numbers from the Regulations alone.

## D. Amendment, and the absence of a veto

15. Holders accept, on subscription, that the Regulations may be amended by the mechanism in clause 16, and that they are bound by the outcome. This is the clause that makes uniform terms possible; without it every holder has a veto over their own contract.
16. Amendments affecting the instrument require a **qualified majority of holders** in a holders' meeting, in addition to the general assembly. Counsel: the machinery of arts. 7:170 ff. WVV is the NV model; confirm availability, majorities and reserved matters for a CV bond issue under art. 6:19, and whether **per-head** voting can be written into the issue conditions.
17. **Future accrual only.** A reduction of `r_I` or `k_I` applies to accrual after the amendment date. Uplift already accrued is honoured. Mirror of [annex-terms clause 13](../option-2-contingent-fee/annex-terms.md), and the condition on which clause 15 is likely to be enforceable at all.
18. A **concentration cap**: no holder may hold more than a stated share of total advances. Adopted whether or not per-head voting is available, since it bounds concentration directly.

## E. Exit, death, succession

19. **Death** or transfer to a **successor vehicle** of the same beneficial owner: the position continues exactly as if the holder were present — accruing while principal is outstanding, and paid to the estate or successor — until closed.
20. **Voluntary withdrawal** is not available at will: the instrument is repaid only out of the waterfall. Any early-repayment right is subject to the solvency test and is a counsel item.
21. **A holder's position is not affected by anything that happens to them as a contributor.** In particular, exclusion for cause on the contributor leg lapses the contributor row and retires `p`; it does **not** touch the bond. That money was real.

## F. Never in the Regulations, an offering document, or a holder statement

- `r` or `k` — the option-2 parameters — in any form, alongside or instead of `r_I` and `k_I`. The two instruments are never described by one parameter, and never appear in the same document. [2026-09-14 mistake](../../../docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).
- Any statement of a contributor's ceiling, the contribution ledger, `p`, or `rem^C / p`.
- A target return, a projected multiple, "beats ETFs", or any figure presented as an expected outcome rather than a cap.
- A promise that a position becomes shares, or that shares will be offered on stated terms later.
- Wording that accrues the uplift as a liability before the board opens `P^I_t` (see clause 23).

## G. Accounting and disclosure

22. **Principal is a liability** of the CV and is booked as one. This is the opposite of the contributor ceiling, which is never booked ([annex-terms clause 27](../option-2-contingent-fee/annex-terms.md)) — and the reason the two instruments must stay separately named.
23. **The uplift is not accrued** until the board opens `P^I_t` and the amount becomes payable. The CV gives its accountant a short written instruction to that effect. If the uplift is accrued, the CV has a fixed liability, the contingency is gone, and the characterisation in clause 2 follows the books rather than the Regulations.
24. The offering document must disclose, at minimum: that repayment is contingent and may never happen; the subordination; that the holder has no vote; the lid and the accrual rate; the amendment mechanism and the absence of an individual veto; the concentration cap; and that contributors, who are the members, vote in the general assembly. Counsel / FSMA: whether an *informatienota* or a prospectus is required (Wet 11 juli 2018; the €5,000,000 / 12-month threshold), and whether a recognised-cooperative exemption applies.
25. Evidence policy: keep the record of every year's waterfall outcome (including `P_t = 0`), every `θ` computation and its inputs, every carry-ledger correction, and every position closed short of its principal. These are the facts a filing relies on.
