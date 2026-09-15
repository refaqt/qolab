# Capped participating bond — the investor leg and the two-leg waterfall (open)

**Status: open (proposed).** The first path in this repo that pays **capital** as well as labour. An investor advances money against a **subordinated, profit-participating bond** whose lifetime return is bounded by a row with the same shape as the contributor cap, and the yearly pool `P_t` is split between the two legs by a formula, not by a vote. It is a **pre-legal spec**: every tax statement below is a DVB hypothesis, not a ruling.

**Prevention rules applied:** [no euro spot price on `p`](../../../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [no day-one lifetime multiple](../../../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md); [no labour-quota cheap shares](../../../docs/mistakes/2026-09-04_cheap-share-euro-par.md) — nothing here is issued for work; [no cap as a balance times `(1 + r)`](../../../docs/mistakes/2026-09-14_cap-as-balance-times-one-plus-r.md); [art. 53, 10° for the excess test](../../../docs/mistakes/2026-09-14_wrong-article-for-excess-test.md); [a second instrument must not publish the comparable the first is designed not to have](../../../docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).

Companion in this folder: [loan-regulations.md](loan-regulations.md) (terms checklist for counsel). Decision: [ADR 2026-09-14 investor leg](../../../docs/decisions/2026-09-14_investor-leg-capped-participating-bond.md). Hardware for experiments: [ADR 2026-09-14 hardware](../../../docs/decisions/2026-09-14_hardware-via-bond-and-loan.md), [2026-09-14 log](../../../docs/log/2026-09-14_hardware-via-bond-and-loan.md). Working notes: [2026-09-14 log](../../../docs/log/2026-09-14_investors-and-the-two-leg-waterfall.md). The labour leg is [option 2](../option-2-contingent-fee/README.md). Symbols: [glossary.md](../../glossary.md). Ruling catalog: [dvb-questions.md](../../analysis/dvb-questions.md).

---

## 1. Why capital needed its own path

Until now QOLAB paid one constituency. [2026-09-10](../../../docs/log/2026-09-10_no-investors-euro-shares.md) settled that there were no investors yet, and the only sketch for them — [cash-subscribed shares](../cash-shares-residual/README.md) — is uncapped and has no rule connecting it to `P_t`.

The requirement was that capital be handled with the **same arithmetic as contributors**: advance `I_i`, receive `d_i`, be bounded by a mirror row. Three routes to a per-investor cap on **shares** were considered and rejected:

| Route | Why not |
| --- | --- |
| Per-share dividend, capped per investor | A dividend must be equal per share inside a *soort*. Paying one holder and not another is not writable without a class difference |
| One class per subscription vintage | A dividend right keyed to issue date creates a *soort* per vintage by operation of law; 10+ live classes, class-by-class votes on every amendment (art. 6:87 WVV), a register tracking vintage. Priced and rejected already in [2026-09-11 §5](../../../docs/log/2026-09-11_cheap-share-ab-classes-sunset.md) |
| A share that amortises to nothing | Forced redemption at par after a bounded stream is the "the share was never equity" fact from [ADR 2026-09-04](../../../docs/decisions/2026-09-04_cheap-share-route-dead-end.md), and a share left with neither profit nor liquidation right raises art. 4:2 |

A **debt instrument** gives each investor their own position, exactly as each contributor has their own row, and the cap becomes an ordinary contract term. Two further consequences fall out, both in the design's favour:

- **The VenB wedge disappears.** A dividend is paid from post-VenB profit; a fee is a deductible cost. Splitting one pool between them in a target ratio means solving `F + Dv/(1−t) ≤ W`, and the ratio is only ever approximately met. A deductible uplift makes both legs pre-tax outflows, so the split in §4 is met **exactly** at leg level.
- **The accountant instruction stops contradicting itself.** [annex-terms clause 27](../option-2-contingent-fee/annex-terms.md) is load-bearing: the contributor ceiling must **never** be booked as a liability. A bond principal **must** be. That is only coherent while the two instruments are named apart (§6).

## 2. Notation

Mirror the contributor row; take no letter that is already spent.

| Symbol | Meaning |
| --- | --- |
| `I_i(n)` | **Cumulative** principal advanced by investor `i` up to and including year `n`. Mirrors `E_i(n)` |
| `ΔI_i(n)` | The year's advance (a flow). Mirrors `e_i(n)` |
| `U^I_i(n)` | **Principal still outstanding** — the base the uplift accrues on |
| `O^I_i(n)` | Accrued but **unpaid** uplift |
| `Ocum^I_i(n)` | Uplift **ever accrued**, never reduced by a payment. This is what the lid binds |
| `rem^I_i(n)` | `U^I_i(n) + O^I_i(n)` — the one number an investor needs |
| `d_i(n)`, `D_i(n)` | Paid on the instrument in year `n`, and cumulative. Covers **principal and uplift together** |
| `r_I`, `k_I` | Investor policy parameters. **Not** `r` and `k` (§6) |
| `θ(n)` | Contributors' share of the year's outflow (§4) |
| `P^C_t`, `P^I_t` | The two legs of `P_t` |

Two collisions to avoid, both of which have bitten this repo before:

- **`U^I` is not the contributor's `U`.** Contributor `U` is *unrecovered effort* and goes to zero when the work has been paid for. `U^I` is an *amortising balance*. Same letter shape, different object — the [glossary](../../glossary.md) says so.
- **`rem^I` is not `S`.** `S` is spent on the rejected 2026-09-07 euro-par burn sketch and stays retired.

## 3. The investor row — no freeze, still capped

The contributor cap freezes because `U = max(0, E(n−1) − A(n))` reaches zero once allocations cover the documented effort. On this leg that would stop the uplift the moment principal is notionally repaid, which is not wanted: money that is still in the company is still at risk. So the row accrues **simple interest on outstanding principal** and a payment **haircuts the whole position proportionally** — the [burn](../option-2-contingent-fee/p-burn-remaining-cap.md) applied to a position instead of to weights.

```
# start of year n
U^I_i        += ΔI_i(n)                                                    # new money
accrual_i(n)  = min( r_I · U^I_i(n−1),  (k_I − 1)·I_i(n) − Ocum^I_i(n−1) )
Ocum^I_i(n)   = Ocum^I_i(n−1) + accrual_i(n)
O^I_i(n)      = O^I_i(n−1)    + accrual_i(n)
rem^I_i(n)    = U^I_i(n) + O^I_i(n)

# after this year's payment d_i(n) ≤ rem^I_i(n)
h             = ( rem^I_i(n) − d_i(n) ) / rem^I_i(n)
U^I_i ← U^I_i · h            O^I_i ← O^I_i · h
```

In one sentence: **everything you advanced and have not been paid back, plus `r_I` per year on the part still outstanding, never more than `k_I` times what you advanced in total.**

Five properties, all of which the formula gives rather than states separately:

1. **Nothing freezes.** The uplift keeps accruing on whatever principal is still outstanding, for as long as any is.
2. **It cannot run away.** Each payment shrinks the accrual base proportionally, so the uplift falls as the position amortises.
3. **The lid still binds the lifetime total, exactly.** Every euro paid comes out of `U^I + O^I`, and the only things ever added to that position are `I` and `Ocum^I`. So over the life of the instrument `D = I + Ocum^I ≤ I + (k_I − 1)·I = k_I · I`. The bound survives with no freeze anywhere.
4. **The 12-month gate survives**, because the accrual multiplies `U^I_i(n−1)`: money advanced this year accrues nothing this year. Mirrors `E_i(n−1)`.
5. **Close-out.** `d = rem` sets `h = 0` and closes the position. Payments alone only approach zero asymptotically, so the regulations state a de-minimis threshold below which the position is paid in full and closed.

### 3.1 The lid is not the freeze, and it stays

Removing the freeze does **not** remove the lid. Without `Ocum^I ≤ (k_I − 1)·I` the instrument is an unbounded claim on all future surplus, which is the hidden-dividend shape in [option-2 §10](../option-2-contingent-fee/README.md) and the expensive failure mode, not the cheap one. It is also the pattern [ADR 2026-09-14](../../../docs/decisions/2026-09-14_simplified-cap-one-row.md) refused when it rejected a ceiling written as a balance times `(1 + r)`. The two objects are different and must never be conflated again:

| | Freeze | Lid |
| --- | --- | --- |
| What stops | The **accrual**, when the thing at risk stops being at risk | The **lifetime total**, at `k ×` the base |
| Contributor leg | Yes — `U = 0` once the work has been paid for | Yes — `cap ≤ k · E` |
| Investor leg | **No** — money in the company stays at risk | Yes — `D ≤ k_I · I` |

### 3.2 Why the legs differ, as a principle

This is not an inconsistency and the path note must not read like one. [Option-2 §5.2 point 3](../option-2-contingent-fee/README.md) calls the freeze *"the single strongest fact in the set"*, because it is what makes the uplift track contingency instead of the calendar. The same rule is applied here to a different thing at risk:

> **Work stops being at risk once it has been paid for. Money stays at risk for as long as it is still in the company.**

Both legs accrue only while the thing at risk is at risk. On the contributor leg that ends at repayment of effort; on the investor leg it ends as the principal amortises. One principle, two consequences.

### 3.3 Worked row

`r_I = 0.25`, `k_I = 3`, €50,000 advanced in year 1.

| Path | Outcome |
| --- | --- |
| Never paid | The uplift accrues €12,500/yr from year 2, reaches the lid in year 9 at `rem^I = €150,000` = 3.00×, and is flat for ever after |
| €12,000/yr from year 3 | The position closes in year 13. Total paid €121,300 = €50,000 principal + €71,300 uplift = **2.43×**, under the lid |

Note what the second row shows: a realistic payment path lands well below the lid. The lid is a bound on the worst case, not a target, and it is not what an arm's-length test will look at (§6).

## 4. The split rule

```
θ(n) = Σ_i rem^C_i(n) / ( Σ_i rem^C_i(n) + Σ_i rem^I_i(n) )

P^C_t = θ(n) · P_t                P^I_t = ( 1 − θ(n) ) · P_t
```

`P_t` keeps the waterfall it already has — `min(policy % of profit or EBITDA, optional revenue cap, cash available after reserves and mission investment)` — computed on profit **before** either leg. Both legs are deductible outflows, so no tax wedge has to be solved around and the ratio is met exactly.

Each leg is then allocated as that leg already prescribes: `P^C_t` splits by `p` and clips at `rem^C` ([option-2 §4](../option-2-contingent-fee/README.md)); `P^I_t` splits across positions and clips at `rem^I`.

### 4.1 The yearly order

With two coupled legs the evaluation order stops being a detail, so it is stated once here and cross-referenced from the option-2 spec:

1. Close the books; compute the base and `P_t`.
2. Roll **both** rows forward on payments **to date**: contributor `U`, `O`, `cap`, `rem^C`; investor accrual, `Ocum^I`, `O^I`, `rem^I`.
3. Compute `θ(n)` from those figures.
4. Split `P_t` into `P^C_t` and `P^I_t`.
5. Allocate within each leg, clipping at each row's remaining amount; burn `p`; haircut `U^I` and `O^I`.
6. One **within-leg** re-pass of anything a capped holder could not absorb. **Never across legs** — `θ` has already priced the relative remaining claims, so cross-leg spill double-counts.
7. Whatever neither leg absorbs stays with the CV for the mission. Record the deviation from `θ` in a carry ledger and correct it in the next year's split.

### 4.2 Degenerate cases

- `Σ rem^I = 0` → `θ = 1`, everything to contributors.
- `Σ rem^C = 0` → `θ = 0`, everything to investors.
- **Both zero** → `θ` is undefined, no leg opens, and the whole of `P_t` stays with the CV. This is the design's endpoint and it deserves naming: **once both legs are capped, the residual belongs to the mission.** That steward-ownership shape is the strongest available non-tax rationale for the whole structure — see DVB **(t)** and [mission.md](../../../docs/mission.md).

### 4.3 Absolute caps mean dilution only delays

A new advance raises `Σ rem^I`, so it lowers every contributor's share of **this year's** flow. It lowers nobody's **lifetime** entitlement, because both caps are absolute euro ceilings rather than shares of a residual. That is the exact opposite of the unbounded dilution that sank the A/B share case in [2026-09-11 §4.2](../../../docs/log/2026-09-11_cheap-share-ab-classes-sunset.md), where the labour class converged on 100% of every future dividend.

### 4.4 Worked example

`r = r_I = 0.25`, `k = k_I = 3`. €10,000 of documented effort accepted in each of years 1–3; €50,000 advanced in year 1; `P_t` = 0, 0, then €20,000, €30,000, then €40,000/yr.

| Year | `rem^C` | `rem^I` | `θ` | `P^C_t` | `P^I_t` | To reserves |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 10,000 | 50,000 | 0.167 | 0 | 0 | 0 |
| 2 | 22,500 | 62,500 | 0.265 | 0 | 0 | 0 |
| 3 | 37,500 | 75,000 | 0.333 | 6,667 | 13,333 | 0 |
| 4 | 36,667 | 71,944 | 0.338 | 10,128 | 19,872 | 0 |
| 5 | 29,840 | 59,511 | 0.334 | 13,359 | 26,641 | 0 |
| 6 | 16,482 | 36,979 | 0.308 | 12,332 | 27,668 | 0 |
| 7 | 4,150 | 10,345 | 0.286 | 4,150 | 10,345 | 25,505 |
| 8+ | 0 | 0 | — | 0 | 0 | 40,000 |

Contributors take €46,635 against €30,000 of documented effort (1.55×, lid 3.00×); the investor takes €97,860 against €50,000 advanced (1.96×, lid 3.00×), and `D = I + Ocum^I` holds to the euro. Both legs close in year 7; from year 8 the whole pool is the CV's to invest in the mission.

Two things to read off the table. First, `θ` is met exactly while both legs have room — year 4 pays 10,128 / 30,000 = 0.338, which is `θ`. Second, `θ` **drifts down** over the run: the contributor leg amortises faster because its accrual freezes while the investor's does not. That drift is the design working, not an error, but it is the number to watch when `r_I` is set.

## 5. Governance: uniform terms, no individual veto

The requirement is that every investor have the **same terms**, that changes be decided **one person, one vote**, and that **no single holder can block** a change. The same is wanted on the contributor side. This changes the sub-route, so it is spelled out.

### 5.1 Bonds, not a stack of bilateral loans

Amending a bilateral contract needs that counterparty's consent. A stack of negotiated loans therefore hands **every lender a veto over their own terms** — precisely what is not wanted. The collective mechanism has to be part of the instrument at the moment of signing:

- **One class, one set of Loan Regulations.** Same `r_I`, `k_I`, waterfall, subordination, close-out and exit rules for everybody; the only things that vary per investor are `I_i` and the year. This mirrors the contributor side, where the QOLAB annex is one standard document and only hours vary.
- A **bond issue carries a holders' meeting** that can bind dissenters by a qualified majority. Counsel item: arts. 7:170 ff. WVV are the NV machinery; whether and how it reaches a CV bond issue under art. 6:19 needs confirming, together with the majorities and which matters are reserved to the meeting.
- Honest cost: a bond is an investment instrument, so the FSMA offer rules apply squarely (§7), and it needs a register.
- **Fallback** if a bond issue is too heavy at the start: bilateral contracts that each incorporate the same Regulations **by reference** and each carry an up-front clause accepting amendment by a stated majority. Weaker than the statutory regime — counsel must confirm enforceability where a majority reduces an existing entitlement.

### 5.2 One person, one vote, in two different rooms

**Amended 2026-09-15.** The members' GA no longer votes one member, one vote. It votes one share, one vote on √-count governance shares with a per-member cap ([ADR 2026-09-15](../../../docs/decisions/2026-09-15_votes-off-the-reward.md), [governance leg](../governance-voting/README.md)). The holders' meeting row below is unchanged.

| Room | Decides | The rule wanted | The obstacle |
| --- | --- | --- | --- |
| **Members' GA** | `P_t` policy, `r`/`k`, `r_I`/`k_I`, the Regulations | One member, one vote | The WVV default attaches votes to shares, so the deviation must be written into the statutes. Counsel confirms the article |
| **Holders' meeting** | Amendments affecting the bond | One holder, one vote | Statutory bondholder voting is normally **by nominal amount**, so a large lender dominates. Different from a veto, but still a concentration of power |

If per-head voting cannot be written into the issue conditions, get the same effect directly: a **concentration cap** — no lender may hold more than a stated share of total advances. Worth adopting either way, and squarely in the cooperative spirit.

### 5.3 No veto is only fair if it is not expropriation

Mirror [annex-terms clause 13](../option-2-contingent-fee/annex-terms.md): a change to `r_I` or `k_I` applies to **future accrual only**. `Ocum^I` already accrued is honoured, as is cap already opened on the contributor leg. Same rule both legs. This is not only fairness — it is also what keeps a majority-amendment clause enforceable when counsel looks at it.

### 5.4 The investor's obvious objection, and its answer

Contributors are the members, so contributors vote on the investors' terms. That is the mirror of the finding in [2026-09-11 §4.3](../../../docs/log/2026-09-11_cheap-share-ab-classes-sunset.md) that uncapped issuance to a class which controls the GA is a continuing value transfer to that class, and a real investor prices it in or refuses.

The answer is that **`θ` is formulaic, not discretionary.** The board decides *how much* is distributed — `P_t`, under the bound discretion the regulation already imposes — and **nobody votes on the split**. Combined with future-accrual-only (§5.3) and the holders' meeting's own consent right (§5.1), the governance surface a member majority can actually move is much smaller than it looks. This is now `θ`'s main governance virtue and should be said out loud in any offering document.

**Lenders are not members and have no GA vote.** That removes the contributors-control-the-GA problem entirely on this instrument and helps the art. 6:1 *coöperatief doel* story. Investors get contractual information rights, not votes.

## 6. `k_I`, and what actually constrains it

The question "is `k = 10` defensible?" has two different answers depending on the leg.

**On the contributor leg it is already answered: no.** [ADR 2026-09-14 two bases](../../../docs/decisions/2026-09-14_two-bases-10x-off-effort.md) puts option 2 at or near 1× because `k × hours × frozen band` hands the administration the comparable (hours × rate), so every euro above 1× must be argued as a risk premium on a wage-like benchmark. Fallback B keeps `k = 10` documented as the honest way to argue it if that decision is reversed, needing evidenced `P_t = 0` years and rows that lapsed unpaid, and expecting DVB to hand the number back as a condition rather than a confirmation. **This path does not reopen that.**

**On the investor leg the base is different** — capital at risk, not hours. There is no wage comparable. A 10× on a successful early investment is an unremarkable outcome that nobody computes an implied rate on.

**But the deduction summons the comparable.** The moment the CV deducts the uplift, the test stops being a venture return and becomes a lending rate: art. 55 WIB 92 (interest deductible only up to market rate) and art. 18, 4° (interest requalified into dividends above market rate, for interest paid to directors or shareholders). So:

> **The deductibility that makes `θ` exact is the same thing that rate-caps `k_I`.**

That is the mirror of the contributor problem and it should be recorded as such, not discovered later.

Four consequences for setting the number:

- **Shape matters more than the lid.** At `r_I = 0.25` the lid needs `(k_I − 1)/r_I` years of total non-payment to bite: 8 years for `k_I = 3`, 36 for `k_I = 10`. Realistic payment paths land far below it — the §3.3 example closes at 2.43× against a 3× lid. What art. 55 tests is the effective rate actually paid, not the lid.
- **Set `r_I` and `k_I` from a documented comparable exercise**, not by mirroring `r` and `k`. The question to answer is what a subordinated, unsecured, contingent-repayment participating loan to a pre-revenue Belgian SME would price at. Separate naming (§6.1) already lets the two pairs diverge later without touching the contributor leg.
- **If a real 10× for capital is wanted**, the consistent move is the one the repo already made for labour: **two bases for capital** — a modest deductible `k_I` on this bond, plus genuinely uncapped equity on the [cash-shares path](../cash-shares-residual/README.md) for investors who want that shape. Open; not decided here.
- `k_I = 10` is flatly incompatible with art. 8:5 WVV recognition *als sociale onderneming* (~6% cap on patrimonial advantage), which [mission.md](../../../docs/mission.md) already flags as undecided. A **capped** return moves the design toward that regime; a large `k_I` moves it out.

### 6.1 Why `r_I` and `k_I` are named apart from `r` and `k`

They may well carry the same values at launch. They are still **separate policy parameters**, never described as "the same parameter" and never stated in the same document.

[Option-2 §5.2](../option-2-contingent-fee/README.md) rests on: *"There is no principal. The contributor supplied work, not money. No loan, no principal, no interest."* On this leg there **is** principal, and §3's accrual is simple interest on a declining balance with payments split between interest and principal. That is correct here and even helpful, because it gives a real arm's-length comparable. The danger is contamination in the other direction: an investor must be told the return terms, and an FSMA *informatienota* compels the disclosure. Publishing *the same named parameter* would hand the administration the proof that `r` is a capital return rate on the contributor leg too.

This is the failure shape [2026-09-11 §4.1](../../../docs/log/2026-09-11_cheap-share-ab-classes-sunset.md) already found once — a second class publishing the euro price of an hour that the first class was designed not to have. Two instances make it a prevention rule: [2026-09-14 mistake](../../../docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).

The same split is why the accountant instruction is coherent: the contributor ceiling is **never** a liability ([clause 27](../option-2-contingent-fee/annex-terms.md)); the bond principal **always** is, while its uplift is not accrued until the board opens `P^I_t`.

## 7. Contingent repayment is load-bearing

- The bond is **subordinated** to all other creditors, has **no fixed maturity** (or a maturity subject to the solvency test), and is repaid **only** out of `P^I_t`. The money is genuinely at risk and an investor may never be repaid.
- That contingency is what buys `k_I > 1`. **If repayment were mandatory, the cap could only cover the uplift and `k_I` would have to fall to a market interest rate.** It is the same argument as the contributor leg: contingency is what buys the multiple, on both.
- **Books:** principal is a liability; the uplift is **not accrued** until the board opens `P^I_t`. If a bookkeeper accrues it, the CV has a fixed liability and the contingency is gone. This is the investor-side mirror of clause 27 and needs the same written instruction to the accountant.
- Prefer **non-transferable** positions, consistent with the rest of the design: no peer market, no secondary trading, off-chain.

## 8. Contributor **and** investor

Rules for a person on both legs. This is where art. 344 §1 bites hardest, because the whole political motive for two instruments is that people who contribute should also share the upside — and the moment what you may advance tracks what you contributed, the split into two boxes looks chosen for its tax result.

1. **Two positions, no netting, no offset.** The person appears in both sums in `θ`.
2. **Anti-correlation.** What a person may advance must not be a function of `c`, `p`, hours, or their contributor row; and `P^C_t` allocation must not be a function of their advance. No document, spreadsheet, MoU, or practice ties the two together.
3. **Cash in must be real money.** Netting an advance against anything the CV owes a contributor is the *inbreng van een schuldvordering* problem from [2026-09-11 §2](../../../docs/log/2026-09-11_cheap-share-ab-classes-sunset.md) wearing debt clothing. Invoice, be paid, then lend — separately and voluntarily.
4. **No pre-agreed reinvestment.** A standing instruction routing fees into the bond reconstructs the labour quota with an extra step.
5. **Exit, death, exclusion follow each leg's own table.** In particular, **exclusion as a bad-leaver contributor must not touch the bond.** That money was real; confiscating it is a different and much worse problem than lapsing a ceiling that was never a receivable.
6. **One vote each room.** A person who is both votes once in the GA as a member and once in the holders' meeting as a holder. The overlap is disclosed and recorded — a standing conflict to manage, not a defect to hide.

### 8.1 Hardware for experiments

A contributor who wants to run an experiment may need hardware or equipment. That cost is **not** documented effort and is **not** paid from `P^C_t`. It is funded on this leg, then used as a company tool. Decision: [ADR 2026-09-14 hardware](../../../docs/decisions/2026-09-14_hardware-via-bond-and-loan.md).

The sequence:

1. The contributor **subscribes to this ordinary bond**, in cash, on the same terms as any other holder.
2. The CV **buys the equipment** from its treasury (which now includes that cash) and **takes title**.
3. The CV **lends the equipment** to the contributor for the experiment (a loan for use; Dutch wording is counsel's: *bruikleen*). This is not the bond. The bond is money lent **to** the CV. The tool is a machine lent **by** the CV.

Why this shape:

- Putting the invoice on `E` would place euros of capital next to hours. That publishes the comparable the labour row is designed not to have.
- Letting the contributor buy and own the tool would leave the machine outside the company. That fights the mission (shared access to manufacturing tools) and leaves the CV with no asset if the person leaves.
- After this sequence the person holds a **subordinated claim**, not the machine. If the CV fails, they stand with the other holders. They cannot take the tool in lieu of repayment.

Guards, all of which follow from §8 and from [the second-instrument rule](../../../docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md):

- **No hardware-bond class.** Same `r_I`, `k_I`, waterfall and close-out as every other holder. Only the amount and the year vary.
- **No earmark in the instrument.** The offering document does not tie a position to a serial number, a project, or a person's hours. The board may still buy a named tool after a subscription; that lives in the purchase file and the loan-for-use contract.
- **The amount is chosen cash**, not a formula of hours, `c`, `p`, or the contributor row. Do not write "€X of tools for Y hours" in any compelled disclosure.
- **Three documents stay apart:** contributor annex, bond offering, loan-for-use contract.
- **Title stays with the CV.** The company may recall the tool, and may lend the same tool to someone else. Exclusion as a contributor does not touch the bond (clause 21); it also does not transfer the machine.
- **Ordinary capex without a matching subscription stays allowed.** This subsection is the path when a contributor wants to put money in so the experiment can have a tool.

Durable equipment is in scope. Consumable materials (items used up in a run) are not decided here.

## 9. What this path does not accept

- Any advance whose size is a function of hours, `c`, `p`, or the contribution ledger. That is the [cheap-share route](../../dead-ends/cheap-share-route.md) in a new instrument.
- Credits converting into bonds, or bonds issued for work rather than for cash.
- An uncapped uplift, or a cap written as a balance times `(1 + r_I)`.
- Cross-leg redistribution of unabsorbed allocations (§4.1 step 6).
- A discretionary split. If the board can vote `θ`, the formula has stopped doing its governance job (§5.4).
- Publishing `r` and `r_I` in the same document (§6.1).
- A special hardware-bond class, a bond issued against equipment rather than cash, or an offering document that matches a position to a serial number (§8.1).
- Adding equipment cost to documented effort, or reimbursing it from `P^C_t`.

## 10. Open questions

- The values of `r_I` and `k_I`, and whether the comparable exercise in §6 puts them at the same numbers as `r` and `k` or apart.
- Whether a real 10× for capital is wanted, and therefore whether **two bases for capital** (§6) is pursued alongside this bond.
- The holders'-meeting machinery for a CV bond under art. 6:19: availability, majorities, reserved matters, and whether per-head voting can be written into the issue conditions (§5.2).
- Enforceability of majority amendment where it reduces an existing entitlement, with future-accrual-only as the protection (§5.3).
- Whether the concentration cap is adopted, and at what percentage.
- The de-minimis close-out threshold (§3, property 5).
- Whether `P_t` should be computed before or after the carry-ledger correction from a prior year (§4.1 step 7).
- Whether a sunset `T` applies on this leg at all. On the contributor leg it stops the opening; here there is no freeze to reach, so a sunset would have to stop the accrual outright. Not drafted.
- Hardware for experiments (§8.1): benefit in kind if the tool is used privately; VAT on the purchase and on a loan for use; whether a modest hire is safer than a free loan; what happens if the tool is destroyed; recall, shared use, and location; whether consumable materials are ordinary project cost.

## 11. DVB items that apply

New: **(t)** art. 344 §1 on the **coupled** waterfall, and **(u)** the participating bond itself. Also **(q)** (rewritten to point at (t)), and **(b)** / **(e)** for the pool. Counsel items from §§5–8.1 are listed in [dvb-questions.md](../../analysis/dvb-questions.md#counsel-items-not-numbered-dvb-items). File for the box, not for the number.
