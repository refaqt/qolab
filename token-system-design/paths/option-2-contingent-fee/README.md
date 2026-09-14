# Option 2 — contingent invoiced fee, `p` as weights (live spec)

**Status: live (next pass).** This is the path the repo is iterating toward: a **contingent success fee** invoiced by the contributor (or their BV, or a project entity), with contribution weights `p` as the split key of a yearly solvency-checked pool. It is a **pre-legal spec**: every tax statement below is a DVB hypothesis, not a ruling. Accepted design pieces have ADRs; the rest is the working sketch consolidated from the logs.

**Prevention rules applied:** [no euro spot price on `p`](../../../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [no day-one lifetime multiple](../../../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md); [no labour-quota cheap shares](../../../docs/mistakes/2026-09-04_cheap-share-euro-par.md); [retire paid-off `p`](../../../docs/mistakes/2026-09-08_unburned-p-after-cap.md); [no *inbreng in nijverheid* for unplanned work](../../../docs/mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md); [art. 53, 10° for the excess test](../../../docs/mistakes/2026-09-14_wrong-article-for-excess-test.md); [no multiple on the effort base](../../../docs/mistakes/2026-09-14_10x-on-the-effort-base.md).

Companions in this folder: [p-burn-remaining-cap.md](p-burn-remaining-cap.md) (accepted), [nested-mint-budgets.md](nested-mint-budgets.md) (accepted), [annex-terms.md](annex-terms.md) (contract terms). Analysis: [belgian-tax-and-company-law.md](../../analysis/belgian-tax-and-company-law.md). Ruling catalog: [dvb-questions.md](../../analysis/dvb-questions.md). Symbols: [glossary.md](../../glossary.md).

Sources consolidated here: [option-2 effort cap (2026-09-04)](../../../docs/log/2026-09-04_option-2-effort-cap.md), [hours-only ledgers and freeze (2026-09-09)](../../../docs/log/2026-09-09_hours-cap-and-project-contractor.md), [`P_t` distribution and cap opening (2026-09-10)](../../../docs/log/2026-09-10_pt-distribution-and-cap-opening.md), [repo review (2026-09-10)](../../../docs/log/2026-09-10_arms-length-10x-and-repo-review.md), ADRs [2026-09-02](../../../docs/decisions/2026-09-02_tax-aware-contribution-credits.md), [2026-09-04](../../../docs/decisions/2026-09-04_fee-cap-not-unit-price.md), [2026-09-08 burn](../../../docs/decisions/2026-09-08_p-burn-remaining-cap.md), [2026-09-08 nested](../../../docs/decisions/2026-09-08_nested-mint-budgets.md), [2026-09-09](../../../docs/decisions/2026-09-09_project-as-contractor.md), [2026-09-14 two bases](../../../docs/decisions/2026-09-14_two-bases-10x-off-effort.md), [2026-09-14 defaults](../../../docs/decisions/2026-09-14_exit-death-and-disallowance-defaults.md).

---

## 1. Ledgers: one input, two columns

| Ledger | What | Job |
| --- | --- | --- |
| Contribution points `c` | `hours × 100`, the same for everyone | Mint weights `p` |
| Documented effort `f` (`E` per lot) | `hours × frozen band`, or a quoted effort in the annex | Invoice **ceiling** at cash-out |

- **Hours** are the one degree of freedom per accepted item (role hours/week, task estimate, project estimate). Log `c` and `f` when the work is **accepted**.
- 100 points/hour only renames hours. It must never be chosen *because* the work is €100/hour; industry rates stay off the points rule.
- **Do not** mint `p` from `f` (that reconstructs `w = df/dp` in €/`p`). **Do not** derive points from euros (`c = f / rate`, `hours = budget / band`, a mint sized from a valuation). `× €1` on dimensionless points is a published par.
- A band is frozen at join / accept (or at contractor join for a project entity). Contract wording: `f` is quoted effort for a **ceiling**; there is no hourly invoice; compensation is a contingent success fee **if** a pool exists. Never “fees he would normally have invoiced.”

## 2. Mint

`p = c0 · c^k` on the **global** curve (early `Δc` mints more `Δp`). `p` is a dimensionless weight: non-transferable, off-chain, no peer market, no euro quote of `dc/dp`, no dashboard of remaining euros per `p`. Transfer only to treasury, on death, or to a successor vehicle of the same beneficial owner (§8).

Sub-projects mint local `p_j` without moving global `c` until the parent spends a mint budget; that root `p` is credited to the **project entity** (§7).

## 3. Pool `P_t`

```
P_t = min(policy % of profit or EBITDA,
          optional revenue cap,
          cash available after reserves and mission investment)
```

- A **flow**, one pot, set each fiscal year. Not an automatic % of turnover. May be **zero**.
- **Bound discretion:** the regulation states the waterfall; the board **shall** open the pool when the waterfall is positive **unless** solvency forbids; named persons then have a payable. Too automatic → a right on surplus (dividend facts, or a receivable). Too discretionary → cannot provision; VenB first.
- **Default-in.** Every eligible holder is allocated. Opt-out or a missed invoice deadline **forfeits** that slice to **operating reserves** — never back into a certificate pot — and still haircuts `p` (§6).
- **Same fiscal year:** work in year `Y` may sit in `P_Y`; invoice in the year of `P_t`, pool quoted **VAT-exclusive**. That is what makes the fee a same-year deductible cost instead of stacked VenB. It also means a year with `P_t = 0` is what keeps contingency real (DVB **(c)**, **(e)**).
- Unallocated profit is Refaqt’s to invest in the mission.

## 4. Payout

```
gross_i = P_t · p_i / Σ p
alloc_i = min(gross_i, max(0, rem_i))        # rem_i = opened cap − paid, before this vintage
invoice_i = alloc_i                          # on default-in; VAT on top
```

`hours × band` is the ceiling, not the invoice. Nobody is owed anything while `P_t` is zero.

## 5. Cap and opening

Per **lot** (one accepted block of work, typically a contribution year), never one blended personal ceiling — new hours must not inherit old waited multiple.

1. **First 12 unpaid months:** opened cap = 1× `E`.
2. **While `paid < E`:** the cap may open further toward `k × E` (opening curve after month 12 is an open question: gated linear or convex).
3. **Freeze when `paid ≥ E`:** stop raising the ceiling. Freeze does **not** forfeit already-opened headroom; `rem = cap − paid` stays invoiceable. Opening after repayment is the rejected trailing coupon.
4. Oldest unpaid lot first (or an explicit junior 1× / senior split stated per lot — open).
5. Optional sunset `T` on top (lapse after `T` vintages unpaid). Bounds duration, not amount. DVB **(g)**.

**The multiple `k` for time-based work is at or near 1×.** Under [ADR 2026-09-14 (two bases, Proposed)](../../../docs/decisions/2026-09-14_two-bases-10x-off-effort.md) option 2 does not carry the large upside: writing the ceiling as `k × hours × frozen band` hands the administration the comparable, so every euro above 1× has to be argued as a risk premium on a wage-like benchmark ([review §1.5](../../../docs/log/2026-09-10_arms-length-10x-and-repo-review.md)). Worked examples in this repo use a small `k` (the older `k = 3` illustration at most); the large upside lives on the [scoped-royalty path](../scoped-royalty-cred-q/README.md) and/or [cash shares](../cash-shares-residual/README.md). `k` and `r` remain GA/board policy parameters, a fee cap, never a published return. Do not book the cap as a receivable; do not call `r` interest.

**Fallback B — gated `k = 10` on effort (documented, not the recommended base).** The 2026-09-10 discussion path (lots; 1× in the first unpaid year; opening so that ~10 fully unpaid years reach 10×; freeze when that lot’s 1× is paid) remains the honest way to argue a large multiple **as a success fee** if the two-bases decision is not taken. If used, file it as one **ex ante** argument: a ceiling that pays 10× only where a lot waited ~10 years fully unpaid, and 0 in every branch where `P_t` never arrives, has an **expected value near 1×** — a no-cure-no-pay contingent fee, not a 26%/year yield. It must be **evidenced**: real years with `P_t = 0`, real lots that lapsed unpaid, and a regulation that does not promise the multiple. The more reliably the pool pays every year, the weaker it gets (tension with **(e)**). Expect DVB to confirm the box and hand the number back as a condition; a later trim of `k` lands on the CV as a partial disallowance (§10), not on the contributor. DVB **(p)**.

## 6. Burn (accepted)

```
if rem_i <= 0:  p_i ← 0
else:           p_i ← p_i · (rem_i − alloc_i) / rem_i
```

Applied every vintage from the start, per lot where lots exist, haircut on `alloc_i` **including forfeited slices**. Invariant: `p / rem` is unchanged by a payout until `rem` hits 0. Full note and guards: [p-burn-remaining-cap.md](p-burn-remaining-cap.md), [ADR 2026-09-08](../../../docs/decisions/2026-09-08_p-burn-remaining-cap.md).

Why this is not a unit price of `p`, in the order to argue it: **first**, a ceiling is not consideration “to be received” (WBTW art. 26) while `P_t` may be zero — remaining `p` is a claim on nothing until a pool exists; **second**, as support, the implied `rem_i / p_i` differs by person and mint date, so it is not a rate that converts every outstanding token the same way. Do not publish `rem / p`. DVB **(i)**, **(j)**.

## 7. Sub-projects (accepted)

Two accepted pieces, one mechanism copied one level down — [nested-mint-budgets.md](nested-mint-budgets.md):

- **Mint gate** ([ADR 2026-09-08](../../../docs/decisions/2026-09-08_nested-mint-budgets.md)): unofficial work logs local `c_j`, `p_j`, personal `f` and does not move parent `c`. The parent spends a point budget `A_{t,j}` / `B_{t,j}` per period; failed projects get 0. Stream, not buyout; never sized from a euro valuation.
- **Cash path** ([ADR 2026-09-09](../../../docs/decisions/2026-09-09_project-as-contractor.md)): the **project entity** holds the root `p`, has a frozen project band and `f_j` = admitted hours × band, invoices `P_t` like a person, and euros land in a **subpool** split by `p_j` and clipped by personal `f`. Contributors do not invoice `P_t` for this work. Fee-cap clock on `f_j` starts at first root-`p` eligibility, not at unofficial accept.

Two levels to start; linear `p_j` first. Someone legal must invoice for a database entity — DVB **(o)**.

## 8. Exit, death, succession (default, Proposed)

Rule for an unpaid opened cap when a holder leaves — [ADR 2026-09-14 defaults](../../../docs/decisions/2026-09-14_exit-death-and-disallowance-defaults.md):

| Event | Opened cap and lots | `p` |
| --- | --- | --- |
| **Death**, or transfer to a **successor vehicle** of the same beneficial owner (BV merger, estate) | Continues **as if present**: the lot keeps opening while unpaid and keeps invoicing (estate / successor invoices) until its cap is exhausted or a sunset hits | Unchanged; burns as euros are taken |
| **Voluntary exit** (resignation, *uittreding*) | Opening **freezes** at the exit date; the already-opened remainder stays invoiceable without time limit | Unchanged; burns as euros are taken |
| **Exclusion** (bad leaver, *uitsluiting*) | The lot **lapses** to operating reserves at the exclusion date | Retired (`p := 0`) |

Same table one level down for the subpool. Membership (governance share) and the credit are separate: leaving the CV as a member does not by itself lapse a lot; the contract governs. Tax: whether a lapse is a taxable event or simply no invoice is DVB **(r)** — the same shape as **(g)**.

## 9. Disallowance risk (default, Proposed)

If the administration later disallows part of a fee as excessive (art. 53, 10° WIB 92), the **pool absorbs** it: the add-back and its VenB are borne by the CV out of reserves and the next `P_t`; there is no clawback from the contributor, whose own tax position is unchanged (they invoiced and were taxed on the full amount either way). Clause text and rationale: [annex-terms.md](annex-terms.md).

## 10. Size drives deductibility; shape drives characterisation

Two different failure modes that earlier notes blurred into one “recharacterisation” fear ([review §1.4](../../../docs/log/2026-09-10_arms-length-10x-and-repo-review.md)):

| Driver | Failure | Who pays | Guard in this spec |
| --- | --- | --- | --- |
| **Size** (`k` too high for the documented work) | Partial disallowance of the **excess** under art. 53, 10°; burden of proof on the administration; VenB on the add-back; a *belastingverhoging* ≥ 10% blocks offsetting losses, DBI, innovation deduction against that supplement (art. 206/3 §1) | The **CV** (§9) | `k` at or near 1× on effort (§5); the large upside on another base |
| **Shape** — membership as the key, points as the key while calling it a dividend, ROI language, unbounded claim on all future surplus | Requalified as **hidden dividend**: no deduction on the whole fee, 30% RV with the **CV as debtor** (grossed up if not withheld), VAT deduction exposed | CV; contributor only if RV is passed on | Points are a fee story; membership share separate; no ROI language; bounded ceiling |
| **Shape** — subordination (time, place, tools, hierarchy, exclusivity) | Requalified as **wage**: employer + employee RSZ, PIT, arrears | Both | Genuine contractors; staff-like people on euro payroll; monthly internal ledger is not an employment contract |

## 11. What this spec does not accept

- Option 1 (dividend on labour-quota shares) — every variant is a [dead-end](../../dead-ends/README.md).
- Unparking [vintage lots](../../parked/vintage-pools.md) as packaging (the lot concept is used; record date `Y+1` and the full vintage machinery are not).
- Any euro par on `p`, transferable `p`, a peer market, a GA-set “price,” `c × €1`.
- A large multiple on the effort base as the recommended design (fallback only, §5).
- Attributing product revenue to projects.

## 12. Open questions

- Opening curve after month 12 (gated linear vs convex) and the value of `r`.
- Oldest-lot-first vs an explicit junior / senior split inside lots.
- Whether sunset `T` sits on top (**(g)**), and its length.
- Who may invoice: BV only, or also *eenmanszaak* / foreign contractors (forcing a BV selects for people who already have a company — see the [adoption constraint](../../README.md#adoption-constraint)).
- Legal invoicing party when a sub-project is a database row (**(o)**).
- Internal fee-cap clock for contributors invoicing a subpool; unused mint budget expires vs rolls (default: expire).

## 13. DVB items that apply

Core **(a)–(d)**; **(e)–(f)** for the yearly pool, default-in and forfeiture; **(h)–(j)** on the ceiling and the burn; **(r)** exit / death; **(p)** only for fallback B; **(g)** if a sunset is used; **(k)–(o)** if nested projects are in scope. Catalog: [dvb-questions.md](../../analysis/dvb-questions.md). File for the box, not for the number.
