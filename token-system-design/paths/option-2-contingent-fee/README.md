# Option 2 — contingent invoiced fee, `p` as weights (live spec)

**Status: live (next pass).** This is the path the repo is iterating toward: a **contingent success fee** invoiced by the contributor (or their BV, or a project entity), with contribution weights `p` as the split key of a yearly solvency-checked pool. It is a **pre-legal spec**: every tax statement below is a DVB hypothesis, not a ruling. Accepted design pieces have ADRs; the rest is the working sketch consolidated from the logs.

**Prevention rules applied:** [no euro spot price on `p`](../../../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [no day-one lifetime multiple](../../../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md); [no labour-quota cheap shares](../../../docs/mistakes/2026-09-04_cheap-share-euro-par.md); [retire paid-off `p`](../../../docs/mistakes/2026-09-08_unburned-p-after-cap.md); [no *inbreng in nijverheid* for unplanned work](../../../docs/mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md); [art. 53, 10° for the excess test](../../../docs/mistakes/2026-09-14_wrong-article-for-excess-test.md); [no multiple on the effort base](../../../docs/mistakes/2026-09-14_10x-on-the-effort-base.md); [no cap as a balance times `(1 + r)`](../../../docs/mistakes/2026-09-14_cap-as-balance-times-one-plus-r.md).

Companions in this folder: [p-burn-remaining-cap.md](p-burn-remaining-cap.md) (accepted), [nested-mint-budgets.md](nested-mint-budgets.md) (accepted), [annex-terms.md](annex-terms.md) (contract terms). The capital leg that shares this pool is the [capped participating bond](../capped-participating-bond/README.md) (open). Analysis: [belgian-tax-and-company-law.md](../../analysis/belgian-tax-and-company-law.md). Ruling catalog: [dvb-questions.md](../../analysis/dvb-questions.md). Symbols: [glossary.md](../../glossary.md).

Sources consolidated here: [option-2 effort cap (2026-09-04)](../../../docs/log/2026-09-04_option-2-effort-cap.md), [hours-only ledgers and freeze (2026-09-09)](../../../docs/log/2026-09-09_hours-cap-and-project-contractor.md), [`P_t` distribution and cap opening (2026-09-10)](../../../docs/log/2026-09-10_pt-distribution-and-cap-opening.md), [repo review (2026-09-10)](../../../docs/log/2026-09-10_arms-length-10x-and-repo-review.md), ADRs [2026-09-02](../../../docs/decisions/2026-09-02_tax-aware-contribution-credits.md), [2026-09-04](../../../docs/decisions/2026-09-04_fee-cap-not-unit-price.md), [2026-09-08 burn](../../../docs/decisions/2026-09-08_p-burn-remaining-cap.md), [2026-09-08 nested](../../../docs/decisions/2026-09-08_nested-mint-budgets.md), [2026-09-09](../../../docs/decisions/2026-09-09_project-as-contractor.md), [2026-09-14 two bases](../../../docs/decisions/2026-09-14_two-bases-10x-off-effort.md), [2026-09-14 defaults](../../../docs/decisions/2026-09-14_exit-death-and-disallowance-defaults.md), [2026-09-14 one-row cap](../../../docs/decisions/2026-09-14_simplified-cap-one-row.md). The one-row cap supersedes the per-lot cap of [ADR 2026-09-03](../../../docs/decisions/2026-09-03_time-opened-fee-cap.md) for this path; working notes: [2026-09-14 simplified cap](../../../docs/log/2026-09-14_simplified-cap-and-r-as-not-interest.md).

---

## 1. Ledgers: one input, two columns

| Ledger | What | Job |
| --- | --- | --- |
| Contribution points `c` | `hours × 100`, the same for everyone | Mint weights `p` |
| Documented effort `f` (`e_i(n)` per year, `E_i` cumulative) | `hours × frozen band`, or a quoted effort in the annex | Invoice **ceiling** at cash-out (§5) |

- **Hours** are the one degree of freedom per accepted item (role hours/week, task estimate, project estimate). Log `c` and `f` when the work is **accepted**.
- **Hardware and equipment are not documented effort.** They do not enter `f`, `E`, `c`, or `p`, and they are not reimbursed from `P^C_t`. When a contributor wants to put money in so an experiment can have a tool, that cash goes through the [capped participating bond](../capped-participating-bond/README.md#81-hardware-for-experiments): the CV buys the tool and lends it. [ADR 2026-09-14 hardware](../../../docs/decisions/2026-09-14_hardware-via-bond-and-loan.md).
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
- **Where an investor leg exists**, `P_t` is **split first** into `P^C_t` and `P^I_t` before anything below happens, and only `P^C_t` is divided by `p` — [capped-participating-bond §4](../capped-participating-bond/README.md). That path also pins the yearly order of operations for both legs; where the two specs describe the same year, its §4.1 governs the sequence.
- Unallocated profit is Refaqt’s to invest in the mission.

## 4. Payout

```
gross_i = P^C_t · p_i / Σ p                  # P^C_t = P_t where there is no investor leg (§3)
alloc_i = min(gross_i, max(0, rem_i))        # rem_i from the row (§5), before this vintage
invoice_i = alloc_i                          # on default-in; VAT on top
```

`hours × band` is the ceiling, not the invoice. Nobody is owed anything while `P_t` is zero. `alloc_i` counts against the row whether or not it is invoiced, so a forfeited slice consumes cap exactly like cash does.

## 5. Cap and opening — one row per contributor

**One row per person, not a set of lots** ([ADR 2026-09-14 one-row cap](../../../docs/decisions/2026-09-14_simplified-cap-one-row.md)). A contributor must be able to answer "what may I still invoice?" with a calculator and this section alone.

| Symbol | Meaning |
| --- | --- |
| `e_i(n)` | Documented effort **accepted in year `n`**: hours × the band frozen at accept, or a quoted effort. A flow. |
| `E_i(n)` | Cumulative documented effort: `E_i(n−1) + e_i(n)`. |
| `a_i(n)` | This vintage's allocation (§4), counted **whether or not it is invoiced**. |
| `A_i(n)` | Cumulative allocations. |
| `U_i(n)` | **Unrecovered effort:** `max(0, E_i(n−1) − A_i(n))`. Work that was already on the books at the start of the year and is still not covered at its end. |
| `O_i(n)` | Accumulated opening. |

```
U_i(n)   = max(0, E_i(n−1) − A_i(n))
O_i(n)   = min( O_i(n−1) + r · U_i(n),  (k − 1) · E_i(n) )
cap_i(n) = E_i(n) + O_i(n)
rem_i(n) = max(0, cap_i(n) − A_i(n))
```

In one sentence: **everything you documented, plus `r` per year of the part that is still unpaid, minus what you were already allocated, and never above `k` times what you documented.**

Four rules that the old per-lot cap had to state separately now follow from the formula:

1. **The 12-month gate.** `U` is built from `E_i(n−1)`, so work accepted this year cannot open until it has survived one full vintage unpaid.
2. **Freeze.** When `A ≥ E` the opening term is zero, so the ceiling stops rising on its own. Freeze does **not** forfeit already-opened headroom: `rem = E + O − A` stays invoiceable. Opening after repayment is the rejected trailing coupon.
3. **Lid.** `O ≤ (k−1) · E`, so `cap ≤ k · E` for life. This replaces the per-lot `k × E_L`.
4. **The opening is linear, not compound.** `r` multiplies unrecovered **effort**, never a running balance. A balance times `(1 + r)` is the arithmetic of a loan; see [mistake 2026-09-14](../../../docs/mistakes/2026-09-14_cap-as-balance-times-one-plus-r.md) and §5.1.

Worked row, `E = €10,000` accepted in year 1, `r = 0.25`, `k = 3`, nothing ever paid:

| Vintage | 1 | 2 | 3 | 5 | 9 | 10+ |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| `cap / E` | 1.00 | 1.25 | 1.50 | 2.00 | 3.00 | 3.00 (lid) |

Paid in full in vintage 2 instead: `U = 0` from that moment, `O` stays where it was, and nothing opens again. Paid €2,000 a year from vintage 2: opening slows as `U` shrinks, freezes in vintage 6 when `A` reaches `E`, and `rem` drains to zero.

### 5.1 Why blending is safe here, and what it costs

A single row cannot tell you **which** work a payment repaid. That is the mechanical reason a per-lot freeze is impossible under a blended cap, and it is why freeze had to be re-derived from `U` instead. Do not reintroduce lots to recover it.

Two further consequences of one row:

- **A parameter change hits everyone at once.** There is no lot vintaging, so a GA/board vote on `r` or `k` moves every contributor's ceiling in the same year. The existing rule still holds: a reduction applies to **future opening** only, and cap already opened is honoured ([annex-terms.md](annex-terms.md) clause 13).
- **Sunset `T` changes shape.** There is no lot to lapse. If a duration bound is still wanted, it stops the **opening** (`O` frozen after `T` years) while `rem` stays invoiceable. The lid is the amount bound. DVB **(g)**, open question.

**The multiple `k` for time-based work is at or near 1×.** Under [ADR 2026-09-14 (two bases, Proposed)](../../../docs/decisions/2026-09-14_two-bases-10x-off-effort.md) option 2 does not carry the large upside: writing the ceiling as `k × hours × frozen band` hands the administration the comparable, so every euro above 1× has to be argued as a risk premium on a wage-like benchmark ([review §1.5](../../../docs/log/2026-09-10_arms-length-10x-and-repo-review.md)). Worked examples in this repo use a small `k` (the older `k = 3` illustration at most); the large upside lives on the [scoped-royalty path](../scoped-royalty-cred-q/README.md) and/or [cash shares](../cash-shares-residual/README.md). `k` and `r` remain GA/board policy parameters, a fee cap, never a published return. Do not book the cap as a receivable; do not call `r` interest (§5.2).

**Fallback B — gated `k = 10` on effort (documented, not the recommended base).** The 2026-09-10 discussion path (lots; 1× in the first unpaid year; opening so that ~10 fully unpaid years reach 10×; freeze when that lot’s 1× is paid) remains the honest way to argue a large multiple **as a success fee** if the two-bases decision is not taken. If used, file it as one **ex ante** argument: a ceiling that pays 10× only where a lot waited ~10 years fully unpaid, and 0 in every branch where `P_t` never arrives, has an **expected value near 1×** — a no-cure-no-pay contingent fee, not a 26%/year yield. It must be **evidenced**: real years with `P_t = 0`, real rows that lapsed unpaid, and a regulation that does not promise the multiple. Note that fallback B was written against the **per-lot** cap and a steeper opening path; reviving it means reviving that machinery as well as raising `k`, so it is now two decisions, not one. The more reliably the pool pays every year, the weaker it gets (tension with **(e)**). Expect DVB to confirm the box and hand the number back as a condition; a later trim of `k` lands on the CV as a partial disallowance (§10), not on the contributor. DVB **(p)**.

### 5.2 `r` is an opening rate, not an interest rate

This is the argument to make, in this order. It is a DVB hypothesis, not a ruling — DVB **(h)**.

1. **There is no principal.** Interest is the price of using a sum of money that was lent or left available. Nothing was lent here. The contributor supplied work, not money. No loan, no principal, no interest — and with no debt, the rules on related-party interest have nothing to attach to.
2. **There is no claim.** `rem` can pay €0 for ever. `P_t` may be zero in any year (§3), and a row may lapse unpaid. A ceiling is not consideration "to be received" (WBTW art. 26) while that is true.
3. **It stops when the risk stops.** Interest on a debt keeps running until the debt is repaid. This ceiling stops opening the moment the work is no longer at risk (`U = 0`). That is what makes the uplift track contingency instead of the calendar, and it is the single strongest fact in the set. The rule is *accrual only while the thing at risk is at risk*, and it is why the [investor leg](../capped-participating-bond/README.md) has **no** freeze: work stops being at risk once it has been paid for, money stays at risk for as long as it is still in the company. One principle, two consequences — not an exception ([path note §3.2](../capped-participating-bond/README.md)).
4. **The thing multiplied is effort, not money.** `O += r · U` prices unrecovered **work**. `cap × (1 + r)` prices a **balance**. The two give similar numbers and are completely different objects — and only one of them is an instrument a reader already has a name for.
5. **State it as a tariff, not as a rate.** "Work still fully unpaid after 1 / 2 / 5 years may be invoiced up to 1.25× / 1.50× / 2.25× its documented effort, never above `k`×" is an ordinary contingent-fee tariff. The same numbers written as a rate on a running total are a loan.
6. **Never let it be booked.** The real exposure is not that a reader is fooled or not fooled. It is that a bookkeeper reaches for the nearest familiar object, puts the ceiling on the balance sheet as a liability, and turns the opening into a financial charge to a related party. Once it is in the books, the tax analysis follows the books, whatever the annex says. This is why the ban on booking the ceiling ([annex-terms.md](annex-terms.md) §F) is load-bearing and needs a written instruction to both accountants.
7. **Words.** Never *interest, rente, intrest, yield, rendement, opbrengst, saldo, tegoed, schuldvordering, achterstal, outstanding, owed, balance, indexation* — in any document on **this** leg, including a contributor statement. (On the [investor leg](../capped-participating-bond/README.md) those words are correct, because that instrument really is debt. The two legs never appear in one document — [2026-09-14 mistake](../../../docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).) Use *ceiling / plafond, opening, unrecovered documented effort, contingent success fee*. "Indexation" is banned on purpose: at this `r` it is nowhere near an inflation story, and inviting that comparison is worse than saying nothing.
8. **The size of `r` moves the risk, it does not remove it.** A rate near a plausible lending rate is the easiest to read as interest. A high `r` is harder to read as interest — no lender earns that on a safe claim — but easier to attack as excessive under art. 53, 10° (§10). That is the better of the two risks, because a partial disallowance is absorbed by the pool (§9). It should be a chosen trade, not an accident.

Do not plan on the administration reading this carelessly. The Dienst Voorafgaande Beslissingen looks at substance and naming will not move it; the box can still be confirmed if the facts support it. Plan for a reader who is right.

## 6. Burn (accepted)

```
if rem_i <= 0:  p_i ← 0
else:           p_i ← p_i · (rem_i − alloc_i) / rem_i
```

Applied every vintage from the start, on the one row, haircut on `alloc_i` **including forfeited slices**. Invariant: `p / rem` is unchanged by a payout until `rem` hits 0. While the row is unpaid `rem` grows, so `p / rem` falls and a later payout burns fewer weights per euro — the **lid** (`cap ≤ k · E`) is what bounds that effect and keeps `p` retiring. Without a lid this term runs away and weight never retires. Full note and guards: [p-burn-remaining-cap.md](p-burn-remaining-cap.md), [ADR 2026-09-08](../../../docs/decisions/2026-09-08_p-burn-remaining-cap.md).

Why this is not a unit price of `p`, in the order to argue it: **first**, a ceiling is not consideration “to be received” (WBTW art. 26) while `P_t` may be zero — remaining `p` is a claim on nothing until a pool exists; **second**, as support, the implied `rem_i / p_i` differs by person and mint date, so it is not a rate that converts every outstanding token the same way. Do not publish `rem / p`. DVB **(i)**, **(j)**.

## 7. Sub-projects (accepted)

Two accepted pieces, one mechanism copied one level down — [nested-mint-budgets.md](nested-mint-budgets.md):

- **Mint gate** ([ADR 2026-09-08](../../../docs/decisions/2026-09-08_nested-mint-budgets.md)): unofficial work logs local `c_j`, `p_j`, personal `f` and does not move parent `c`. The parent spends a point budget `A_{t,j}` / `B_{t,j}` per period; failed projects get 0. Stream, not buyout; never sized from a euro valuation.
- **Cash path** ([ADR 2026-09-09](../../../docs/decisions/2026-09-09_project-as-contractor.md)): the **project entity** holds the root `p`, has a frozen project band and `f_j` = admitted hours × band, invoices `P_t` like a person, and euros land in a **subpool** split by `p_j` and clipped by personal `f`. Contributors do not invoice `P_t` for this work. Fee-cap clock on `f_j` starts at first root-`p` eligibility, not at unofficial accept.

Two levels to start; linear `p_j` first. Someone legal must invoice for a database entity — DVB **(o)**.

## 8. Exit, death, succession (default, Proposed)

Rule for an unpaid opened cap when a holder leaves — [ADR 2026-09-14 defaults](../../../docs/decisions/2026-09-14_exit-death-and-disallowance-defaults.md):

| Event | The row | `p` |
| --- | --- | --- |
| **Death**, or transfer to a **successor vehicle** of the same beneficial owner (BV merger, estate) | Continues **as if present**: the row keeps opening while `U > 0` and keeps invoicing (estate / successor invoices) until `rem` is exhausted or a sunset hits | Unchanged; burns as euros are taken |
| **Voluntary exit** (resignation, *uittreding*) | `r := 0` from the exit date, so `O` stops growing; the already-opened remainder stays invoiceable without time limit | Unchanged; burns as euros are taken |
| **Exclusion** (bad leaver, *uitsluiting*) | The row **lapses** to operating reserves at the exclusion date (`cap := 0`) | Retired (`p := 0`) |

One row makes this simpler than the per-lot version it replaces: three events, three one-line effects. Same table one level down for the subpool. Membership (governance share) and the credit are separate: leaving the CV as a member does not by itself lapse a row; the contract governs. Tax: whether a lapse is a taxable event or simply no invoice is DVB **(r)** — the same shape as **(g)**.

## 9. Disallowance risk (default, Proposed)

If the administration later disallows part of a fee as excessive (art. 53, 10° WIB 92), the **pool absorbs** it: the add-back and its VenB are borne by the CV out of reserves and the next `P_t`; there is no clawback from the contributor, whose own tax position is unchanged (they invoiced and were taxed on the full amount either way). Clause text and rationale: [annex-terms.md](annex-terms.md). A cash reserve for this is treasury, not a deductible provision; size it to tax on the excess for **open years only** (3-year ordinary clock) — [2026-09-14 no-ruling log](../../../docs/log/2026-09-14_no-ruling-reserve-and-lookback.md).

## 10. Size drives deductibility; shape drives characterisation

Two different failure modes that earlier notes blurred into one “recharacterisation” fear ([review §1.4](../../../docs/log/2026-09-10_arms-length-10x-and-repo-review.md)):

| Driver | Failure | Who pays | Guard in this spec |
| --- | --- | --- | --- |
| **Size** (`k` too high for the documented work) | Partial disallowance of the **excess** under art. 53, 10°; burden of proof on the administration; VenB on the add-back; a *belastingverhoging* ≥ 10% blocks offsetting losses, DBI, innovation deduction against that supplement (art. 206/3 §1) | The **CV** (§9) | `k` at or near 1× on effort (§5); the large upside on another base |
| **Shape** — membership as the key, points as the key while calling it a dividend, ROI language, unbounded claim on all future surplus | Requalified as **hidden dividend**: no deduction on the whole fee, 30% RV with the **CV as debtor** (grossed up if not withheld), VAT deduction exposed | CV; contributor only if RV is passed on | Points are a fee story; membership share separate; no ROI language; bounded ceiling |
| **Shape** — subordination (time, place, tools, hierarchy, exclusivity) | Requalified as **wage**: employer + employee RSZ, PIT, arrears | Both | Genuine contractors; staff-like people on euro payroll; monthly internal ledger is not an employment contract |

## 11. What this spec does not accept

- Option 1 (dividend on labour-quota shares) — every variant is a [dead-end](../../dead-ends/README.md).
- Unparking [vintage lots](../../parked/vintage-pools.md). The lot concept is now retired for this path too: the cap is one row per contributor (§5). Record date `Y+1` and the full vintage machinery stay out.
- A ceiling written as a running balance times `(1 + r)`: unbounded, it deletes freeze, and it is the arithmetic of a loan ([mistake 2026-09-14](../../../docs/mistakes/2026-09-14_cap-as-balance-times-one-plus-r.md)).
- Any euro par on `p`, transferable `p`, a peer market, a GA-set “price,” `c × €1`.
- A large multiple on the effort base as the recommended design (fallback only, §5).
- Attributing product revenue to projects.
- Hardware or equipment on the effort row, or reimbursed from `P^C_t`. That cost is capital: [capped-participating-bond §8.1](../capped-participating-bond/README.md#81-hardware-for-experiments).

## 12. Open questions

- The values of `r` and `k`. Worked examples use `r = 0.25` and `k = 3`; neither is set. `k` is what makes the whole thing filable, so it cannot stay open for ever.
- Whether a sunset `T` sits on top (**(g)**), and its length. Under one row it stops the opening, it does not lapse a lot (§5.1).
- Whether the contributor statement (§5.2 point 7, [annex-terms.md](annex-terms.md) clause 24) needs a fixed template before anyone receives one.
- Who may invoice: BV only, or also *eenmanszaak* / foreign contractors (forcing a BV selects for people who already have a company — see the [adoption constraint](../../README.md#adoption-constraint)).
- Legal invoicing party when a sub-project is a database row (**(o)**).
- Internal fee-cap clock for contributors invoicing a subpool; unused mint budget expires vs rolls (default: expire).
- Interaction with the [investor leg](../capped-participating-bond/README.md) if it is adopted: `θ` drifts down over a run, because this leg's opening freezes while the capital leg's accrual does not. That is the design working, but it is the number to watch when `r_I` is set.
- Whether consumable materials (items used up in an experiment) are ordinary project cost, or something else. Durable equipment is on the [bond path §8.1](../capped-participating-bond/README.md#81-hardware-for-experiments).

## 13. DVB items that apply

Core **(a)–(d)**; **(e)–(f)** for the yearly pool, default-in and forfeiture; **(h)–(j)** on the ceiling and the burn, with **(h)** rewritten for the one-row cap and now also asking the accounting question (§5.2 point 6); **(r)** exit / death; **(p)** only for fallback B; **(g)** if a sunset is used; **(k)–(o)** if nested projects are in scope. Catalog: [dvb-questions.md](../../analysis/dvb-questions.md). File for the box, not for the number.
