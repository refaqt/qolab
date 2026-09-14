# ADR — Exit, death, succession and disallowance: contract defaults

- **Date:** 2026-09-14
- **Status:** Proposed (contract terms for counsel; tax treatment is DVB item **(r)**).
- **Amends:** [ADR 2026-09-02](2026-09-02_tax-aware-contribution-credits.md) point 3 (transfers only to treasury, on death, or to a successor vehicle) by saying what happens to an **unpaid opened cap** in each case. Adds the disallowance allocation the [2026-09-10 review §4.3](../log/2026-09-10_arms-length-10x-and-repo-review.md) found missing.
- **Does not accept** option 1 vs 2 (still option 2 for this pass). Does not unpark vintages. Does not revive any dead-end.

## Context

The live option-2 machinery (`p`, lots, opened cap, freeze, burn) had no rule for what happens to an unpaid opened cap when a contributor leaves or dies — a contract gap and a tax question of the same shape as DVB **(g)**. Separately, nobody had written down who bears a partial disallowance at the CV under art. 53, 10° WIB 92 (add-back, VenB on it, and the art. 206/3 §1 ban on offsetting losses against a supplement with a ≥ 10% tax increase): the pool, or the contributor via clawback.

Both are contract terms, not tax questions. Options considered on 2026-09-14 — exit: continue as if present / freeze then lapse after `T` / lapse immediately; disallowance: pool absorbs / clawback of the excess / decide with counsel. Session: [2026-09-14 log](../log/2026-09-14_review-followups-and-path-restructure.md).

## Decision

Defaults for the QOLAB annex — [annex-terms.md §C–D](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md), [option-2 spec §8–9](../../token-system-design/paths/option-2-contingent-fee/README.md):

1. **Death, or transfer to a successor vehicle of the same beneficial owner:** the lot **continues as if the holder were present** — it keeps opening while unpaid and keeps invoicing (estate / successor invoices) until its cap is exhausted or a sunset, if any, hits. `p` unchanged; burns as euros are taken.
2. **Voluntary exit** from the contractor relationship: opening **freezes** at the exit date; the already-opened remainder stays invoiceable without time limit.
3. **Exclusion** for cause: the lot **lapses** to operating reserves; `p` retires. Grounds are listed in the annex.
4. The same three rules apply one level down for subpool euros of a sub-project. Membership and the credit are separate: leaving as a member does not by itself change a lot.
5. **Disallowance: the pool absorbs it.** Tax at the CV from a partial disallowance of a fee that remains a fee is borne by the CV out of operating reserves and, if needed, the next `P_t`. No clawback, no credit note; the contributor's tax position is unchanged. A later reduction of `k` applies to future opening; already-opened cap is honoured (ask in **(p)** whether a clawback would be expected).
6. If a payment is **requalified** (hidden dividend, wage), the annex allocates RV / RSZ per the statutory debtor; whether RV may be passed on is a counsel item.

## Consequences

- Estates and successor BVs are ordinary creditors under the same contingent fee, not new grantees; nothing is “waived” on freeze or lapse because the ceiling was never a receivable. That is the working hypothesis to file as **(r)**.
- Every holder bears a disallowance pro rata through a smaller future `P_t`; nobody is asked to repay a fee they were taxed on. This matches the review's finding that size drives deductibility at the CV, not the contributor's tax.
- The ledger needs an exit-state per lot (active / frozen / lapsed) and a successor field per holder.
- Counsel drafts the clauses; the DVB filing describes them as facts.
