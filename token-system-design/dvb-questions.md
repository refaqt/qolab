# DVB questions (a)–(q)

Catalog of questions to put to the **Dienst Voorafgaande Beslissingen** (and counsel / accountant) before anyone is promised QOLAB credits or paid under them. This is **design input**, not a ruling and not a substitute for a filing.

Numbering is stable. **(a)–(d)** are the core option-2 box. **(e)–(h)** were written for parked vintage packaging; they still apply wherever the live spec uses a yearly `P_t`, default-in, forfeiture, or a time-opened cap. **(i)–(j)** bind the next option-2 pass. **(k)–(o)** are nested sub-projects. **(p)** is the 2026-09-10 opening path (`k = 10`, lots, first-year 1×). **(q)** is the general anti-abuse rule on a two-instrument split.

**Working hypothesis until a ruling:** VAT and professional income attach at **invoice**, not at mint; cash-out is an option-2 **success fee**, not a dividend; `p` is a dimensionless weight; the effort cap is an invoice ceiling, not a unit FX (`€/p`). Substance beats labels.

**Which article does what** (corrected 2026-09-10 — [review log](../docs/log/2026-09-10_arms-length-10x-and-repo-review.md)). Earlier notes cite **art. 49 WIB 92** for “not excessive.” Art. 49 sets the **conditions** of deductibility (incurred in the period to obtain or retain taxable income, and justified). The **excess** test is **art. 53, 10° WIB 92** (*kosten in zover zij op onredelijke wijze de beroepsbehoeften overtreffen*): burden of proof on the administration, **partial** rejection only, no review of opportuneness. **Art. 26 WIB 92** (abnormal or benevolent advantage) has an express carve-out where the advantage **is taken into account in determining the taxable income of the Belgian recipient** — so it is largely neutral for a contributor or contributor BV that invoices and is taxed; art. 26 §2 targets related foreign / privileged-regime recipients. Quantum risk therefore runs through **art. 53, 10°** and through **requalification**, not through art. 26.

**What a ruling can and cannot settle.** The DVB rules on the **legal treatment** of a described transaction and issues decisions for **at most five years**, binding only while the stated conditions hold and the facts were completely and correctly described; the KB of 17 January 2003 already excludes tax rates and the calculation of tax. Expect the **box** ((a)–(e)) to be confirmable and the **quantum** (`k`) to come back as a *condition* (“provided the remuneration is at arm’s length”) rather than a confirmation. Prefiling is informal and non-binding; a negative signal there normally ends as *zonder gevolg* and the request is amended or dropped. A formal negative decision cannot be appealed, only refiled in modified form before the transaction is executed. **There is no mechanism by which the DVB orders a cap of 3× or any other multiple.**

Companion analysis: [token-system.md](token-system.md), [vintage-pools.md](vintage-pools.md), [p-burn-remaining-cap.md](p-burn-remaining-cap.md), [nested-mint-budgets.md](nested-mint-budgets.md). Session that restated the live opening path: [docs/log/2026-09-10_pt-distribution-and-cap-opening.md](../docs/log/2026-09-10_pt-distribution-and-cap-opening.md).

---

## Index

| Item | One-line question | Live? |
| --- | --- | --- |
| **(a)** | Is mint of non-transferable `p` a taxable event? | Yes |
| **(b)** | Is cash-out a fee/royalty or a dividend? | Yes |
| **(c)** | When is VAT due (mint, work performed, or invoice)? | Yes |
| **(d)** | Contractor vs employee / RSZ (arbeidsrelatie)? | Yes |
| **(e)** | Same-year deduction of a default-in `P_t` allocation? | Yes if yearly pool |
| **(f)** | Forfeiture of uninvoiced / opt-out slices (and haircut of `p`)? | Yes |
| **(g)** | Opened cap vs sunset as the lifetime bound? | If sunset is used |
| **(h)** | Time-opened cap vs interest / receivable? | Yes |
| **(i)** | Effort cap vs implied `€/p` at grant? | Yes |
| **(j)** | Proportional `p` burn vs remaining consideration? | Yes |
| **(k)** | Taxable event at local accept, first root `p`, or invoice (nested)? | If nested |
| **(l)** | Is local `p_j` a non-claim on parent `P_t`? | If nested |
| **(m)** | Parent mint budgets vs implied euro value of the project? | If nested |
| **(n)** | Fee-cap clock on `f_j` from first root `p`, not unofficial years? | If nested |
| **(o)** | Project entity invoices `P_t`; people invoice the subpool? | If nested |
| **(p)** | `k = 10` after ~10 unpaid years, 1× in year 1, lots: still a fee? | Proposed path |
| **(q)** | Art. 344 §1 abuse on splitting labour (fee) from residual upside (shares)? | If two instruments |

---

## (a) No taxable event at mint

**Question.** Does logging hours, minting contribution points `c`, and minting non-transferable weights `p = c0 · c^k` create Belgian income tax or VAT **at grant**, or only later when an invoice exists?

**Why it exists.** Belgian practice on tokens, warrants and benefits looks at **vesting + ability to dispose**, not at later conversion into cash. VAT (WBTW arts. 22, 26; VAT Directive art. 73) taxes everything received **or to be received**, including non-cash, at value, if there is a direct link (Tolsma, C-16/93). A published euro rate on `p` (`w = dc/dp`, `v = pool / N`, 1 `p` = €1) is the failure mode: then mint looks like consideration **now**.

**Case to file.** Off-chain ledger; `p` non-transferable except treasury / death / successor vehicle of the same beneficial owner; no peer market; no euro quote of `dc/dp`; no dashboard of remaining euros per `p`; pool `P_t` may be zero; contract says compensation is a contingent success fee **if** a pool exists.

**Working hypothesis.** A mere hope (no pool, no claim, no market) can stay untaxed at mint. That is **not** a guarantee. Logging `f` (hours × frozen band) as a **reference ceiling** must not read as an unissued invoice (see **(h)** and **(i)**).

**Ask DVB.** Confirm no PIT/VAT at mint of `c`/`p`/`f` under those facts. If they disagree, ask **which** fact creates the event (the points, the weights, or the euro ceiling).

---

## (b) Cash-out: fee vs dividend

**Question.** When the contributor invoices `a_i` from `P_t`, is that a **professional fee / royalty** (option 2: deductible for the CV, VAT 21%, PIT/social or BV VenB) or a **dividend** (option 1: after-tax profit, WVV tests, 30% roerende voorheffing, not deductible, no VAT on a genuine distribution)?

**Why it exists.** You cannot have both “not a dividend” and “not a fee.” Renaming does not help. Allocation by **contribution points** is the smoking gun that the cause is **labour**, not a return on a small membership share. A normal CV that pays those people from surplus is not volunteer work (Wet 3 juli 2005). VVPRbis does not apply to work-minted “profit certificates.”

**Case to file.** Option 2 wrapper: dienstenovereenkomst + IP/CLA + QOLAB annex; `P_t = min(policy % of profit or EBITDA, optional revenue cap, cash after reserves)`; GA/board **shall** open that pool when the waterfall is positive **unless** solvency forbids (bound discretion); named persons then have a payable; invoice same fiscal year; leftover to **operating reserves**, not a certificate pot; membership share is **separate** and does not set the payout.

**Tightrope.**

| Too automatic | Too discretionary |
| --- | --- |
| “`P_t` **is** x% of profit every year, split by `p`.” Looks like a **right on surplus** → dividend facts, or an unconditional debt (grant-time / receivable). | “We pay if we feel like it.” No certain liability → cannot provision → VenB first; later payment may be after-tax or another year. |

**Working hypothesis.** Points-minted `p` is a **fee story**. Option 1 is the weaker characterisation. A mix (FPS treat the excess as hidden profit distribution) is the worst case: deduction denied, WHT and/or PIT, VAT may still be claimed, increases.

**Ask DVB.** Characterise `a_i` as a contractual success fee. Confirm it is **not** a distribution on capital, including if the CV is or becomes a social enterprise. Ask what would flip it (automatic %, membership as the key, ROI language, unbounded claim on all future surplus).

---

## (c) VAT time of supply

**Question.** If option 2 holds, is VAT due (i) when work is performed, (ii) when `p` or `f` is logged, or (iii) when the success-fee invoice is issued because `P_t` crystallised?

**Why it exists.** Art. 22 WBTW: a service is taxable when performed. Art. 26: taxable amount includes what is to be received. A **genuine** contingent fee can wait until the fee exists. An arrangement that is **in substance this year’s hours × rate, billed in December** is a delayed ordinary invoice → VAT as the work was done.

**Case to file.** Contract: no hourly invoice; `f` is quoted effort for a **ceiling**; pay only if a pool exists; pool specified **VAT-exclusive**. Some years `P_t` can be zero. Same-year invoice when a vintage **does** run (needed for **(e)**).

**The backstop to argue against (art. 22bis WBTW).** For a B2B service, VAT is chargeable when the invoice is issued **and in any case on the fifteenth day of the month following the month in which the art. 22 taxable event occurred**, if no invoice was issued before that date. “We invoice when `P_t` exists” therefore defers nothing **by itself**. The defence must be that the **service is not yet completed** (continuous / staged supply) or that the **consideration is genuinely conditional and undetermined**, so no chargeable amount exists yet — the line supported by CJEU *baumgarten sports & more* (C-548/17) on conditional successive payments. File it that way; do not let counsel find the backstop first.

**Working hypothesis.** VAT on the **invoice** in the year of `P_t` if contingency is real. `Y+1` record date does **not** move VAT to next year if FPS recharacterise as ordinary 2026 services. Rates are the same either way; **timing** changes.

**Ask DVB.** Time of supply for the success fee. Confirm logging `f` is not a supply. Confirm a year with `P_t = 0` creates no VAT.

---

## (d) RSZ / arbeidsrelatie

**Question.** Are QOLAB contributors **self-employed contractors** (or a BV) invoicing a success fee, or **employees** (loonbeschermingswet: salary in euro; tokens as benefit in kind; employer + employee RSZ + PIT)?

**Why it exists.** Arbeidsrelatiewet looks at **subordination** (time, place, tools, hierarchy, exclusivity), not at monthly vs yearly logging. Freelancers may invoice monthly. A timesheet plus a December payment of hours × band inside a CV that directs the work is classic wage, whatever the contract is called. Volunteer-member labour in a profit-distributing CV is a poor fit.

**Case to file.** Employees on euro payroll; QOLAB is not wages in kind. Contractors genuinely independent (other clients, no subordination). Monthly **internal** hours ledger is the input to `c` and `f`, not an employment contract.

**Working hypothesis.** Genuine freelance + one yearly success-fee invoice + monthly credits on an internal ledger can be option 2. Staff-like people must be on payroll. A monthly ledger does **not** by itself create employment; subordination does.

**Ask DVB / social counsel.** Confirm the contractor pattern. Ask where the line is if someone works near-full-time only for Refaqt.

---

## (e) Same-year deduction of a default-in vintage

**Question.** If the regulation allocates `a_i` by default and the person invoices in the **same fiscal year** as the profit that funded `P_t`, may the CV deduct that amount as a professional expense of **that** year (art. 49 WIB 92)?

**Why it exists.** Option 2 avoids stacked VenB **only** if the fee is a same-year deductible cost. If money sits as retained earnings and is paid later, Refaqt pays VenB first; later deduction may miss. Parked `Y+1` (work in `Y` invoices from `P_{Y+1}`) **hurts** this: 2026 profit may be taxed before the 2027 invoice. The 2026-09-10 discussion chose **work in `Y` can sit in `P_Y`** and **invoice in the same fiscal year** as `P_t`.

**Case to file.** Bound waterfall (see **(b)**); default-in; invoice deadline in year `t`; leftover to reserves. Illustrative numbers: €10,000 profit before the fee, €5,000 invoiced in year `t` → deduction in `t`.

**Working hypothesis.** Same-year invoice is the correct option-2 timing. It does **not** change the tax **rate** vs `Y+1`; it changes **when** the CV deducts. It also makes “mere hope until a future vintage” weaker for **this year’s** work (see **(c)**).

**Ask DVB.** Deductibility in year `t` of default-in allocations that are invoiced in year `t`. What if the invoice arrives after year-end but before the filing date?

---

## (f) Forfeiture of opt-out / uninvoiced slices

**Question.** If a person is defaulted-in, allocated `a_i`, and does **not** invoice by the deadline, that slice goes to **operating reserves** and nobody can claim it later. Must `p` (and remaining cap) still be reduced as if they had taken it? Is the forfeited amount income to the CV, a waived receivable, or never a payable?

**Why it exists.** If leftover of `P_t` recycled into a certificate pot, holders wait for a fatter `v` (idle pool). If uninvoiced slices **do not** haircut `p`, sitting out a thin year preserves weight for a fat year. If `Fr`/`O` are not reduced, skipping also **grows opening** (`O += Fr × r`).

**Worked case (haircut on allocation, not on cash).** Two people, equal `P = 100`, `cap = €5,000`. Year 1 `P_t = €2,000` → `a = €1,000` each. Alice invoices. Bob does not; €1,000 → reserves.

| | Bob’s `P` not burned | Both burned on `a` |
| --- | ---: | ---: |
| After year 1 | Alice 80, Bob **100** | Both 80 |
| Year 2 `P_t = €50,000` | Bob takes a larger share | Same weight |

**Working hypothesis.** Default-in plus forfeiture to reserves is required for the flow (not stock) model. Haircut `p` **and** apply `a_i` to remaining cap whether or not cash is paid. Tax characterisation of the forfeit (never a payable vs waived income) needs a ruling.

**Ask DVB.** Treatment at the CV and at the contributor. Confirm the haircut is not a taxable disposal of `p` at a euro par (see **(j)**).

---

## (g) Opened cap vs sunset as the bound

**Question.** If lots lapse after `T` vintages unpaid (sunset), is that the lifetime bound for tax, or is the **opened effort cap** the bound that matters? Does sunset create a forfeiture event?

**Why it exists.** Unlimited lifetime share of every future `P_t` is equity-like. A fat year inside `T` would still fill a **static** `k×` if opening were not time-gated. Sunset does not replace the opened cap.

**Case to file.** Only if the spec keeps a sunset `T` on top of the opened cap. The 2026-09-10 path uses lots + freeze + `k`; sunset is optional.

**Working hypothesis.** The invoice ceiling is the opened cap. Sunset is a second, contractual lapse, not a unit price.

**Ask DVB.** If sunset is in the regulation, whether lapse is a taxable event or simply no invoice.

---

## (h) Time-opened fee cap vs interest / receivable

**Question.** Opening extra cap while principal is unpaid (`O` grows with time, `r` a parameter, only while `Fr > 0` / `paid < E`) — is that **interest on a balance**, a **growing receivable**, or still only a **ceiling** on a future contingent invoice?

**Why it exists.** WBTW art. 26: taxable amount includes what is to be received. Booking `cap` as a CV liability or contributor receivable crystallises euros without cash. Describing `r` as interest invites roerende voorheffing on the `O` slice. Opening after `paid ≥ E` is the rejected trailing coupon / gold rush and looks like interest on a repaid balance.

**Cases.**

| Construction | Interest / receivable optics |
| --- | --- |
| `r` as “yield”; dashboard “€X still owed”; book debt | Strong — avoid |
| Proportional paydown of remaining principle `F` and `O` like a loan | Strong — **discarded** 2026-09-09 |
| `O += Fr × 0.08` **per month** from month 1 (~2× at first `P_t`) | Strong yield path — not the filing version |
| Per **lot**: 1× for 12 unpaid months, then open toward `k×` only while that lot’s principal is unpaid; freeze when `paid ≥ E`; do not book a receivable; do not call `r` interest | Intended filing version |

**Working hypothesis.** A ceiling is not consideration to be received while `P_t` may be zero. FPS look at substance, not the word “cap.” Year-1 freeze and freeze-after-1×-paid are what make it look like a **wait-dependent fee bound**, not a loan.

**Ask DVB.** Explicitly: time-opened cap with **year-1 at 1×** and later opening vs interest / receivable. Confirm no income as `O` accrues.

---

## (i) Effort fee cap vs implied `€/p` at grant

**Question.** Does `pay ≤` opened cap on documented effort `E` (hours × frozen band) imply a grant-time unit price `(k × E) / Δp`, so VAT/PIT attach at mint?

**Why it exists.** If that quotient were a unit FX (euros per token, the same for every outstanding `p` at a date), it would be the same class of fact as `w`, `v = P/N`, and 1 `p` = €1. The design claim: the cap is on the **invoice versus work**, not on minted `p`. Same work, different mint dates, same cap, different `Δp` — the quotient is not a property of `p`. A maximum is not value: if `P_t` is zero, nothing is owed. Static `k×` open on day one plus a forecasted fat pool looks more like ascertainable consideration of ~`k×E`.

**Working hypothesis.** An effort-tied fee cap is **not** a unit FX. Lead with the **ceiling** argument — a maximum is not consideration “to be received” while `P_t` may be zero — and use the non-uniformity of the quotient (same work, different mint dates, different `Δp`) as **support**, not as the case; an auditor can simply decline to be impressed by the algebra, and the `p` burn has since made remaining `p` linear in remaining opened cap ([p-burn-remaining-cap.md](p-burn-remaining-cap.md)). Do **not** publish `(k × E) / Δp` or `rem / p`. Do not mint `p` from `f` (that reconstructs `w = df/dp` in €/`p`). Logging `f` is safe only as a **contractual ceiling document**, not “fees he would normally have invoiced.”

**Ask DVB.** Effort-tied cap vs implied `€/p` at grant. Cover uniform 100 points/hour (hours renamed, not €100/hour). Cover **`k = 10`** as still a fee bound (see **(p)**).

---

## (j) Proportional burn of `p` vs remaining consideration

**Question.** Each vintage: `alloc_i = min(P_t · p_i / Σ p, rem_i)`; `p_i ← p_i · (rem_i − alloc_i) / rem_i`; `rem_i = 0 ⇒ p_i = 0`. Operationally remaining `p` is **linear** in remaining opened cap. Is remaining `p` remaining **consideration**, or still a dimensionless weight plus an invoice ceiling?

**Why it exists.** Euro-par burns (`cash / w`, `v = P/N`, 1 `p` = €1, `S ← S − €`) price the mint. This fraction does not convert tokens at one rate for everyone; implied €/`p` is `rem_i / p_i`, which differs by person and mint date. It is still **stronger grant-time evidence** than never burning `p`. Do not publish `rem / p`. Do not book remaining `p` as remaining euros. Haircut on **`alloc_i`**, including forfeited slices.

**Working hypothesis.** The burn amortizes **weight** as the ceiling is consumed. It is not a unit FX. Accepted as design ([p-burn-remaining-cap.md](p-burn-remaining-cap.md)); tax characterisation open.

**Ask DVB.** Remaining `p` after the fraction: still not a euro claim? Confirm the haircut is not a disposal at par.

---

## (k) Delayed root-`p` mint after unofficial nested work

**Question.** Sub-project `j` may log local hours/`c_j`/`p_j` before the parent admits any root `p`. Is there a taxable event at **local accept**, at **first `B_{t,j} > 0`** (parent mint budget spent; entity becomes a contractor on `P_t`), or still only at **invoice**?

**Why it exists.** Recognition is a more sensitive grant-time moment than ordinary mint: “we now believe this project.” Still a hope until `P_t` exists. Unofficial calendar time must not open the euro cap (**(n)**).

**Working hypothesis.** No tax until invoice, even at first root `p`, if there is no euro par and no receivable. First `B_{t,j} > 0` is the moment FPS might disagree.

**Ask DVB.** Three-point timeline: local accept / first root `p` / invoice.

---

## (l) Local `p_j` is not a claim on `P_t`

**Question.** Is `p_j` only a **split key for euros already in `j`’s subpool**, with no claim on parent `P_t`, or do holders of `p_j` have a right on the parent pool?

**Why it exists.** Direction A (distribute parent `p` to people inside `j`) was rejected. If `p_j` is treated as already “worth a share of Refaqt,” that is a priced claim at local mint.

**Working hypothesis.** Only **root** `p` (people or project entities) shares in `P_t`. `p_j` cannot invoice `P_t`.

**Ask DVB.** Confirm `p_j` is not a parent-pool right.

---

## (m) Parent mint budgets vs implied project value

**Question.** The parent chooses how many points to admit (`A_{t,j}` / `B_{t,j}`). Does that choice **imply a euro value** of the project (especially at a commercialisation vote), so tax attaches as if the project were valued?

**Why it exists.** Sizing `B_{t,j}` from a euro valuation of the project, or `c × €1`, is a published par. Admitted hours × **project band** → `Δf_j` is the intended cap object, not a valuation.

**Working hypothesis.** A point budget is a dilution gate, not a price, if it is not derived from euros.

**Ask DVB.** Mint budgets in points vs implied project value.

---

## (n) Fee-cap clock at first root `p`

**Question.** Does opening of `f_j` / remaining cap start at **local accept** (including unofficial years) or only at **first root-`p` eligibility** for the project?

**Why it exists.** A sale year plus years of “unpaid opening” on wilderness hours recreates a day-one lifetime multiple ([gold rush](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md)). Unofficial years do not open the euro cap.

**Working hypothesis.** Clock starts at first root `p`. Catch-up of backlog is an attested hour inventory, then a parent admit at the **project** rate.

**Ask DVB.** Confirm unofficial logging is not already opening a euro claim.

---

## (o) Project entity invoices `P_t`; people invoice the subpool

**Question.** May the **project** (as the contractor at parent level) invoice `P_t` into a euro subpool, with contributors invoicing **that subpool** (split by `p_j`, clipped by their own `f`), not parent `P_t`? What if the “entity” is a **database row** rather than a separate legal person?

**Why it exists.** Parent should not accept individual sub-project tasks or blend contributor rates into a lump. Two invoice hops have VAT and art. 49 consequences. A database label cannot be a VAT debtor; someone legal must invoice.

**Working hypothesis.** Design math: project-as-person at parent, people on the subpool. Implementation must name a legal invoicing party (CV, a BV, or the contributors on a disclosed split). Tax characterisation of the subpool as a mere cost centre vs a supply between entities is open.

**Ask DVB.** Project-entity invoice; contributor invoices to the subpool; what is required if there is no separate company for `j`.

---

## (p) `k = 10`, lots, first-year 1× — fee or equity-like return?

**Question.** Intended opening path after the 2026-09-10 discussion: **per lot**; **cap = 1× `E`** for the first 12 unpaid months; then open so that **~10 unpaid years → 10×**; freeze further opening when that lot’s `paid ≥ E` (already opened remainder stays payable); leftover `P_t` to reserves; option 2 invoice. Is that still a **bounded success fee on documented work**, or an **investment / profit right** (too close to unbounded residual equity, or to a 26%/year compound return on unpaid effort)?

**Why it exists.** `k = 3` in older examples was a conservative illustration, not a legal maximum. `k = 10` after a long dry period is a **startup-equity-shaped** upside. 8% **per month** from month 1 already gives ~2× at the first `P_t` and looks like a yield (**(h)**). An **uncapped** share of all future `P_t` is residual claimant ≈ shareholder, unlike a salesperson’s 10% of **their** subscriptions. A cap that is so high it never binds can be ignored as decoration → mix of option 1 and 2 (deduction denied on the excess, WHT, possible VAT still on the “fee” story).

**Path vs lid (illustrative, `cap / E`):**

| Unpaid years | 8%/month from month 1 | 1× for 1 year, then linear to 10× at year 10 | Convex `1 + 9 (t/10)^2` |
| ---: | ---: | ---: | ---: |
| 1 | 1.96 | 1.00 | 1.09 |
| 2 | 2.92 | 2.00 | 1.36 |
| 5 | 5.80 | 5.00 | 3.25 |
| 10 | 10 | 10 | 10 |

**Working hypothesis.** Lots + year-1 1× + freeze-after-1×-paid make 10× **defensible as a fee bound** for true long unpaid wait. They do **not** guarantee DVB blesses `k = 10`. Do not publish 10× or `r` as ROI or “beats ETFs.” ETF return is return on **cash already received**; the multiple is catch-up because cash was **not** received. If DVB trims `k`, the same machine still works.

**The argument to actually file (ex ante, not ex post).** Arm’s length is tested on the **bargain at the time it was struck**, not on the winning branch. A ceiling that pays 10× **only** where a lot waited ~10 years **fully unpaid**, and **0** in every branch where `P_t` never arrives, has an **expected value near 1×**. That is a no-cure-no-pay contingent fee, not a 26%/year yield. The pieces are already in the spec (`P_t` may be zero; lots lapse unpaid; freeze after 1× paid; no opening after repayment) — file them as one argument. It must be **evidenced**: real years with `P_t = 0`, real lots that lapsed unpaid, and a regulation that does not promise the multiple. Note the tension with **(e)**: the more reliably the pool pays every year, the weaker this gets.

**Base of the ceiling is the real problem, not the number.** Writing the cap as `k × hours × frozen band` hands FPS the comparable (hours × rate), so every euro above 1× must be defended as a risk premium **on a wage-like benchmark**. A **royalty scoped to the products that embody the contribution** is compared against royalty rates instead, and a 10× lifetime return on the effort is then an ordinary outcome nobody computes. See the [review log](../docs/log/2026-09-10_arms-length-10x-and-repo-review.md) §1.5 and the [Cred/Q path](../docs/log/2026-09-10_cred-value-q-euro-par.md).

**If the multiple is later disallowed, the CV pays — not the contributor.** Under **art. 53, 10°** only the **excess** slice is rejected: Refaqt has already paid the cash **and** owes VenB on the add-back, while the contributor’s tax is unchanged (they invoiced, they are taxed either way). Worse, a *belastingverhoging* of 10% or more on that supplement blocks the offset of losses, DBI, innovation deduction and the other deductions listed in **art. 206/3 §1 WIB 92** against it — which matters for a cooperative carrying forward losses. The contributor only pays more if the payment is **requalified** (hidden dividend → 30% RV with the CV as debtor; or wage → RSZ + PIT), and that is driven by **shape** (membership as the key, points as the key, subordination), not by the size of `k`. **Nothing in the draft annex says who bears a disallowance** — pool or contributor. Write it.

**Ask DVB.** Together with **(h)** and **(i)**: whether this path is still option 2; whether `k = 10` is at arm’s length (**art. 53, 10°**, with art. 49 for the conditions) after a long **unpaid** wait; whether a lower multiple would be required for a short payback (already 1× in year 1 under this path); **and whether they will confirm a quantum at all** or only the characterisation. Ask explicitly what happens to **already-opened** cap if `k` is trimmed later — is the contract still enforceable, and is a clawback expected.

---

## (q) Art. 344 §1 — splitting labour and residual upside across two instruments

**Question.** If labour is paid as an option-2 contingent fee (credits `p`, effort cap, invoice) **beside** a residual 10×-shaped upside on **cash-subscribed shares**, can FPS invoke **art. 344 §1 WIB 92** (*fiscaal misbruik*) to treat the two together as one arrangement — a labour-quota profit right — and tax it accordingly?

**Why it exists.** The general anti-abuse rule is not in any earlier note in this repo. It is the natural attack on structure A from the [tokens-not-shares log](../docs/log/2026-09-10_tokens-not-shares-avoid-revisor.md): the whole political motive for the two-instrument split is that contributors who work more should also get more of the residual. The moment the share allocation correlates with contribution — in the statutes, in a members’ agreement, in an MoU, or only in practice — the split into two legal boxes starts to look chosen for its tax result. That is the same family of fact as every [cheap-share](cheap-share-route.md) rejection, one level up.

**Case to file.** The share class count is defensibly **not** `f(p)`: equal per contributing member, or a fixed statutory split against an investor class, with a **non-tax reason** for that shape (governance, one-member-one-vote, admission policy) that would hold even if the tax outcome were reversed. Credits never convert into shares. No document ties share count to hours, points, `p`, or a contribution ledger.

**Working hypothesis.** Two genuinely different bases (capital at risk vs documented work), each with its own non-tax rationale, is not abuse. A share count that tracks contribution is the labour quota with an extra step, and art. 344 §1 is how it gets unwound even where company law was respected.

**Ask DVB / counsel.** Whether the two-instrument split survives art. 344 §1 on the facts filed. Ask what correlation between contribution and share count is tolerated (eligibility gate vs quantum).

---

## Related screens (not numbered DVB items)

| Topic | Safer pattern |
| --- | --- |
| MiCA | Off-chain, no technical peer transfer (Recital 17) |
| E-money | No euro unit / par |
| FSMA / prospectus | No ROI language; no offer of an investment to non-members |
| DAC8 | No public crypto rails |

---

## How to file

Put **draft contracts** (dienstenovereenkomst + QOLAB annex), the **waterfall** for `P_t`, and **worked numbers** (including a year with `P_t = 0` and a year that fills opened cap) in the ruling request. Ask **(a)–(d)**, **(e)–(f)**, **(h)–(j)**, and **(p)** on the live path; add **(g)** if sunset is in the spec; add **(k)–(o)** if nested projects are in scope; add **(q)** if a second, share-based instrument is in scope.

**File for the box, not for the number.** Start at **prefiling**. The gate before launch is **(a)–(d)**, not **(p)**: those are the expensive risks (tax at mint, dividend, wage, VAT timing) and they are the ones a ruling can actually close. Treat a decision that confirms the mechanism while leaving arm’s length as a condition as a **success**, not a failure — the residual exposure is then a partial disallowance at the CV under art. 53, 10°, which is the cheapest of the failure modes. Do not delay launch waiting for a confirmation of `k = 10` that the service is unlikely to give.

Until the ruling exists, do not promise a unit price, a target ROI, a pot that “will be worth more if you wait,” or a default `k×` on a short payback.
