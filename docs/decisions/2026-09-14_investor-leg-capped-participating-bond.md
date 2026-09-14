# ADR — The investor leg is a capped participating bond, split against contributors by formula

- **Date:** 2026-09-14
- **Status:** Proposed (pending counsel and a DVB prefiling). Nothing is launched or offered by this ADR.
- **Amends:** the "do not publish `r`" constraint in the [path map](../../token-system-design/README.md) and in [`.agents-local/rules/repo.md`](../../.agents-local/rules/repo.md), with a second narrow carve-out for an investor offering document. Amends [option-2 §3–§4](../../token-system-design/paths/option-2-contingent-fee/README.md): `P_t` is now split before it is allocated by `p`.
- **Supersedes:** nothing. The [cash-shares path](../../token-system-design/paths/cash-shares-residual/README.md) stays open and is now also the home of the **uncapped** capital base if a large multiple for capital is ever wanted.
- **Does not change:** the mint `p = c0 · c^k`, the waterfall that computes `P_t`, default-in and forfeiture, the [one-row contributor cap](2026-09-14_simplified-cap-one-row.md) or its **freeze**, the [fractional burn of `p`](2026-09-08_p-burn-remaining-cap.md), the [nested mint budgets](2026-09-08_nested-mint-budgets.md), or the [project-as-contractor cash path](2026-09-09_project-as-contractor.md).
- **Does not decide:** the values of `r_I` and `k_I`; whether a second, uncapped capital base is pursued; whether a bond issue or bilateral contracts are used at launch; whether a sunset applies on this leg.
- **Does not revive:** [cheap shares](2026-09-04_cheap-share-route-dead-end.md), [bonding-curve shares](2026-09-07_bonding-curve-shares-dead-end.md), or [*inbreng in nijverheid*](2026-09-10_inbreng-in-nijverheid-dead-end.md). **Does not reopen** [two bases](2026-09-14_two-bases-10x-off-effort.md): option 2 stays at or near 1× on effort.

## Context

QOLAB paid one constituency. [2026-09-10](../log/2026-09-10_no-investors-euro-shares.md) settled that there were no investors yet, and the only sketch for them — cash-subscribed shares — is uncapped and has no rule connecting it to the pool. The requirement now is that capital be handled with the **same arithmetic as contributors**: advance `I_i`, receive `d_i`, be bounded by a mirror row, and split the yearly pool between the two legs in the ratio of what each leg may still be paid.

Three routes to a per-investor cap on **shares** were considered and rejected, because a dividend must be equal per share inside a *soort*: capping per investor is not writable; a class per subscription vintage costs 10+ live classes and a class vote on every amendment (already priced in [2026-09-11 §5](../log/2026-09-11_cheap-share-ab-classes-sunset.md)); and a share that amortises to nothing is the "the share was never equity" fact from [ADR 2026-09-04](2026-09-04_cheap-share-route-dead-end.md).

A debt instrument gives each investor their own position, as each contributor has their own row, and the cap becomes an ordinary contract term. Two consequences fall out in the design's favour. The **VenB wedge disappears**: a deductible uplift makes both legs pre-tax outflows, so the split is met exactly rather than approximately, which is what a dividend leg could never do. And the **accountant instruction stops contradicting itself**: the contributor ceiling must never be booked as a liability ([annex clause 27](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md)), while a bond principal must be — coherent only while the two instruments are named apart.

Three refinements came out of the design conversation and are the substance of this ADR.

1. **The freeze does not belong on the investor leg.** Carrying the contributor formula over unchanged would stop the uplift the moment principal was notionally repaid. Work stops being at risk once it has been paid for; money stays at risk for as long as it is still in the company.
2. **Uniform terms need a collective amendment mechanism built into the instrument.** Amending a bilateral contract needs that counterparty's consent, so a stack of negotiated loans hands every lender a veto over their own terms.
3. **`k_I` is constrained by the deduction, not by the base.** On capital at risk a large multiple has no wage comparable and is an unremarkable outcome. The moment the CV deducts the uplift, the comparable becomes a lending rate.

## Decision

Until counsel and a DVB prefiling say otherwise:

1. **The investor leg is a subordinated, profit-participating bond**, repaid only out of the waterfall, with no fixed maturity, non-transferable, carrying no vote in the general assembly, and subscribed in **cash only**. Nothing on this leg is ever issued for work, and what a person may advance is never a function of hours, `c`, `p`, or the contribution ledger.

2. **The row accrues without freezing, and is still capped.** For holder `i` in year `n`:

   ```
   accrual_i(n) = min( r_I · U^I_i(n−1),  (k_I − 1)·I_i(n) − Ocum^I_i(n−1) )
   Ocum^I_i(n)  = Ocum^I_i(n−1) + accrual_i(n)
   O^I_i(n)     = O^I_i(n−1)    + accrual_i(n)
   rem^I_i(n)   = U^I_i(n) + O^I_i(n)

   # after this year's payment d_i(n)
   h = ( rem^I_i(n) − d_i(n) ) / rem^I_i(n)
   U^I_i ← U^I_i · h        O^I_i ← O^I_i · h
   ```

   `U^I` is outstanding principal, `Ocum^I` is uplift ever accrued. A payment reduces principal and accrued uplift in the same proportion — the [burn](2026-09-08_p-burn-remaining-cap.md) applied to a position instead of to weights.

3. **The lid survives the removal of the freeze, exactly.** Every euro paid comes out of `U^I + O^I`, and the only things ever added to that position are `I` and `Ocum^I`, so over the life of the instrument `D = I + Ocum^I ≤ k_I · I`. The lid is **not** the freeze, and it stays: without it the instrument is an unbounded claim on all future surplus, which is the hidden-dividend shape and the expensive failure mode.

4. **The pool is split by formula, not by vote.**

   ```
   θ(n) = Σ rem^C_i(n) / ( Σ rem^C_i(n) + Σ rem^I_i(n) )
   P^C_t = θ(n) · P_t          P^I_t = (1 − θ(n)) · P_t
   ```

   `P_t` keeps its existing waterfall, computed before either leg. Unabsorbed amounts re-pass **within a leg only**; whatever neither leg absorbs stays with the CV for the mission; deviations are carried and corrected the following year. The yearly order of operations is stated once, in [the path note §4.1](../../token-system-design/paths/capped-participating-bond/README.md).

5. **`r_I` and `k_I` are separate policy parameters from `r` and `k`**, defaulted to the same values at launch, never described as the same parameter and never stated in the same document. They should be set from a documented comparable exercise — what a subordinated, unsecured, contingent-repayment participating loan to a pre-revenue Belgian SME would price at — rather than by mirroring the contributor parameters.

6. **The publication rule gains a second carve-out.** An **investor offering document** may state `r_I`, `k_I` and the cap, because disclosure is compulsory and an investor cannot be asked for money without the return terms. It may not state `r`, `k`, any contributor ceiling, or the contribution ledger. Public and promotional material, and any return or yield framing outside a compelled disclosure, stay banned.

7. **Uniform terms, amendable by majority, with no individual veto.** One class, one set of [Loan Regulations](../../token-system-design/paths/capped-participating-bond/loan-regulations.md); only the amount and the year vary per holder. Holders accept on subscription that the Regulations may be amended by a qualified majority in a holders' meeting alongside the general assembly. One member, one vote is written into the statutes for the general assembly. A **concentration cap** bounds any single holder's share of total advances, adopted whether or not per-head voting is available at the holders' meeting.

8. **Amendment is future-accrual-only.** A reduction of `r_I` or `k_I` applies to accrual after the amendment date; uplift already accrued is honoured, as is cap already opened on the contributor leg. This is both the fairness rule and the condition on which a majority-amendment clause is likely to be enforceable.

9. **Contingent repayment is load-bearing and must be preserved in the books.** Principal is a liability; the **uplift is not accrued** until the board opens `P^I_t`. The CV instructs its accountant in writing to that effect. If repayment were ever made mandatory, the cap could only cover the uplift and `k_I` would have to fall to a market interest rate.

10. **File two new DVB items:** **(t)** art. 344 §1 on the coupled waterfall, and **(u)** the participating bond itself. **(q)** is rewritten to point at (t).

## Consequences

- Capital and labour are both bounded, and the residual belongs to the CV and the mission. That **steward-ownership** shape is now the design's strongest non-tax rationale under art. 344 §1 — a corporate-purpose choice that holds if the tax outcome were reversed — and it comes from [mission.md](../mission.md) rather than from a tax result.
- **`θ` does governance work, not only arithmetic.** The obvious investor objection is that contributors are the members and therefore vote on the investors' terms. The answer is that the board decides how much is distributed and nobody votes on the split.
- **Dilution only delays.** Because both caps are absolute euro ceilings, a new advance lowers everyone's share of this year's flow but nobody's lifetime entitlement — the opposite of the unbounded dilution that sank the A/B share case in [2026-09-11 §4.2](../log/2026-09-11_cheap-share-ab-classes-sunset.md).
- **The two legs now read as one principle, applied twice:** the uplift accrues only while the thing at risk is at risk. That has to be stated wherever the freeze is explained, or the option-2 argument looks abandoned.
- **A new tension is on the record:** the deductibility that makes `θ` exact is the same thing that rate-caps `k_I`. If a real 10× for capital is wanted, the consistent answer is two bases for capital — a modest deductible `k_I` here plus uncapped equity on the cash-shares path — not a larger `k_I` on a deductible instrument.
- **A new class of risk is named.** A second instrument can publish the comparable the first was designed not to have. This is the second instance ([2026-09-11 §4.1](../log/2026-09-11_cheap-share-ab-classes-sunset.md) was the first), so it becomes a [prevention rule](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).
- **FSMA is now live.** A bond offered beyond members is an offer of investment instruments, with an *informatienota* or prospectus question attached. Earlier paths could stay in member-only territory; this one cannot, by design.
- Bonds over bilateral loans is a cost as well as a choice: an investment instrument, a register, and formal issuance. The bilateral fallback exists but is weaker on exactly the point that motivated the change.
- `k_I` cannot stay open for ever, for the same reason `k` cannot: it is what makes the leg filable.
