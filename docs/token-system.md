# QOLAB contribution-credit system (Belgian law)

Working analysis of the proposed Refaqt token system under Belgian VAT, income tax, company law, and EU financial regulation. This is **design input for counsel and an accountant**, not a ruling and not a substitute for a Dienst Voorafgaande Beslissingen (DVB) ruling.

**Prevention rules applied:** none yet in `docs/mistakes/` (folder empty). Token-engineering rule that applies here: do not treat “token” labels as taking compensation outside VAT or income tax.

## Direct answers

| Question | Working answer |
| --- | --- |
| Conversion of U-tokens into euros: dividend or supplier cost? | **Can be a supplier cost** if it is consideration for documented services under a contract, paid to the person who did the work. It **looks like a dividend / profit right** if tokens are transferable, priced in euro, or paid because someone holds a claim on surplus rather than because they supplied work. Facts beat labels. |
| Must contributors be members of the cooperative? | **No, not for the reward contract.** Membership is a governance choice. Mixing membership and token cash-out makes recharacterization as a surplus distribution more likely. |
| Internal tokens, but contributors may sell R and U to each other? | **Avoid.** A secondary market is the single fastest way to give R-tokens a taxable value on grant, and it pushes the design toward FSMA / MiCA / e-money analysis. |
| What contract does Refaqt have with contributors? | A **services agreement** (dienstenovereenkomst / aanneming van werk) plus IP terms, with a contingent success-fee annex. Employment contracts if there is authority. Tokens must not be wages in kind for employees (loonbeschermingswet). |
| Avoid VAT when receiving R-tokens (no cash yet)? | **Possible only if R is not consideration** — no euro price, no market, no par claim, no right to dispose. The current bonding-curve + U=€1 + peer sales design **fails** that test. |
| Avoid income tax when receiving R-tokens? | Same test. Belgian practice taxes token-for-work when the right **vests and the holder can dispose of it**, not when it is later swapped for euros. |

---

## Goals (as stated)

1. Reward contributions to Refaqt **when there is revenue**.
2. **Cap** rewards.
3. Contributors get a **higher return** than initial hourly rate × hours.
4. Rewards **scale with how well Refaqt is doing**.

Those four goals are compatible with Belgian tax **if** the euro payment is a **deferred, contingent success fee for services**. They become hard if the system looks like an investment in Refaqt.

---

## How the current design works (as described)

```
work → C-tokens (effort or time)
     → bonding curve → R-tokens (scarcer as total contributions grow)
     → optional burn at curve price → U-tokens (1 U = 1 euro)
     → when revenue: 10% of revenue into a pool
     → holders offer U; euros = pool × U_offered / total_U_offered
     → unused U converted back to R at the prior conversion price
     → euro payout = invoice to Refaqt, VAT charged
```

Early contributions get more R for the same effort (power-law mint). Cash only appears if there is a pool and a holder burns into a distribution round.

---

## VAT — when, and how much

### Legal hooks

- Taxable event for services: when the service is **performed** (art. 22 WBTW).
- Chargeability: generally when the **invoice** is issued; at the latest the 15th of the following month if no invoice; earlier on **prepayment** (art. 22bis WBTW).
- Taxable amount: everything received or to be received, **including non-cash**, at market value (art. 26 WBTW; VAT Directive art. 73).
- Standard rate for professional services: **21%**.
- Small-enterprise exemption (art. 56bis WBTW): Belgian turnover **≤ €25,000** (2026) — no VAT charged, no input deduction. Invoice must state the exemption.
- Intra-EU B2B services to a Belgian taxable person: usually **reverse charge** (contributor invoices 0% with reverse-charge mention; Refaqt accounts for Belgian VAT and deducts if entitled).

Paying in tokens does **not** take the supply outside VAT. Hedqvist (C-264/14) exempts exchanging bitcoin-like currency for fiat as a financial transaction. It does **not** exempt services paid in tokens.

### Two competing VAT maps

**Map A — R-tokens are the consideration (current design, high risk)**

Work is supplied now; R (and the right to convert R→U→euro) is what the contributor receives. Then:

| Moment | VAT |
| --- | --- |
| Grant of R (or of freely convertible R) | **Likely due.** Taxable amount = euro value of R. A bonding-curve price and a 1 U = €1 peg are evidence of that value. |
| Peer sale of R or U | Possible second taxable supply (assignment / barter), messy. |
| Invoice at euro cash-out | If VAT was already due at grant, this is adjustment / residual, not the first chargeable event. |

This is the outcome to avoid: VAT (and often income tax) while the contributor has **no euros**.

**Map B — R-tokens are not consideration (target design)**

R is an internal, non-transferable **ranking weight**. The only consideration is a **contingent euro fee** that exists only when Refaqt opens a pool and allocates a cash amount. Then:

| Moment | VAT |
| --- | --- |
| Recording R | None, if there is no ascertainable consideration and no disposal right. |
| Allocation + invoice for euros | **Yes.** Taxable amount = the invoiced euro fee (VAT exclusive). |

EU case law on genuinely contingent success fees (successive payments, VAT Directive art. 64) supports charging VAT when the fee **crystallises**, not when the work was done. Artificial delay of a already-fixed fee does **not** get that treatment.

**The current design sits on Map A** because it publishes a conversion price, pegs U to euro, and allows peer sales.

### How much VAT at a clean cash-out (Map B)

Assume a Belgian contributor, normal VAT regime, pool allocation of **€10,000 net** (VAT exclusive — specify this in the rules).

| | Amount |
| --- | --- |
| Fee (taxable amount) | €10,000 |
| VAT 21% on the invoice | €2,100 |
| Contributor bills Refaqt | €12,100 |
| Refaqt input VAT | Recoverable if Refaqt is a taxable person with a right of deduction |
| Contributor remits to FPS | €2,100 (cash-flow neutral if the customer pays) |

If the contributor is under the small-enterprise regime: invoice **€10,000**, mention art. 56bis, **no VAT**.

If the contributor is an EU taxable person established outside Belgium: typically reverse charge; Refaqt self-accounts 21% and deducts according to its recovery right.

**Specify in the rules that the pool is VAT-exclusive.** If the pool is “€10,000 including VAT”, the net fee is €10,000 / 1.21 ≈ €8,264 and VAT is €1,736. Mixing VAT-registered and exempt contributors in one pro-rata pool without this rule will treat them unequally.

Employees: salary must be paid in legal tender (Wet 12 april 1965). A token grant is still a taxable benefit; it is a poor fit for this system. Pay employees in euro; keep QOLAB for genuine contractors and member-contributors who invoice.

---

## Income tax and social charges — when, and how much

### When (Belgium)

For token-for-work, Belgian practice (and DVB questionnaires) looks at **definitive vesting + effective disposal**, not at the later euro conversion. A common misconception — “tax only when I sell to euros” — is **wrong** if the tokens already have value and can be sold or converted.

| Holder | When taxed | On what | Typical burden (indicative, 2026) |
| --- | --- | --- | --- |
| Employee | When the benefit is granted / vested | Benefit in kind at market value | PIT progressive to 50% + municipal + **RSZ** (employer + employee) |
| Self-employed natural person | When the fee is earned / invoiced; for tokens, at vesting if they have value | Professional income (art. 23–24 WIB 92) | PIT progressive to 50% + municipal, **social contributions ~20.5%** (deductible for PIT). All-in often ~55–65% of net fee at the top rate |
| Belgian company (BV/CV) of the contributor | Accrual when the right is certain | VenB 20% SME band / 25% | No RSZ on the company; salary taken out later is a separate event |
| Private investor selling crypto | Realisation | **Not this system.** Work tokens are professional income first. From 2026, private crypto gains: 10% above €10,000 exemption if “normal management”; 33% + municipal if speculative | Do not design as if contributors were investors |

If R has **no market, no peg, no unconditional claim**, the professional-income event can be argued to occur only at **invoice / cash-out**. That is the whole point of stripping price and transferability out of R.

If the contributor later holds leftover value (they should not, in the target design), any extra gain is a **separate** analysis (professional vs miscellaneous vs 10% capital-gains). Do not rely on the 10% crypto CGT: tokens received for work start as professional income.

### Dividend withholding is not a shortcut

Standard dividend withholding is **30%** (roerende voorheffing). The old extra exemption for recognised cooperatives is now folded into a general dividend exemption of **€833** per person per year (assessment year 2026), claimed on the PIT return, not at source. VVPRbis and liquidation-reserve regimes are about **share capital**, not work tokens.

Calling a work payout a dividend to get 30% instead of ~60% is the wrong optimisation: it is often **recharacterised**, it is **not deductible** for Refaqt, and it fights the “payment for work” story.

---

## Dividend or supplier cost?

Substance over form. Belgian tax looks at what was paid **for**.

| | Supplier cost (target) | Dividend / surplus (to avoid for this flow) |
| --- | --- | --- |
| Legal basis | Contract for services; contingent fee | Return on shares; GA distribution; net-asset / liquidity tests (WVV) |
| Deductible for Refaqt VenB? | **Yes**, if professional and arm’s-length enough | **No** |
| VAT | Yes, on the fee (unless exemption / reverse charge) | No (out of scope as a distribution) |
| Contributor tax | Professional income + social (or VenB) | 30% WHT (+ tiny exemption) |
| Who can receive | Anyone who supplied the work (member or not) | Shareholders |
| Need profit? | No — but paying 10% of **revenue** can exceed profit | Yes, after tax, with tests |
| Recognised CV as social enterprise (art. 8:5 WVV) | Fees to suppliers are not “vermogensvoordeel on shares” | Any advantage **in whatever form** to shareholders can hit the ~6% cap on paid-in capital — a token surplus paid to member-holders is a statute risk |

A **10% of revenue** pool is economically a **revenue share / royalty**, not a dividend. That supports cost treatment **if** it is consideration for identified work. It also supports **investment** treatment if anyone can buy R and sit on the 10% without working.

**Ristourne (patronage refund)** is a third bucket: a price adjustment based on transactions with the cooperative, sometimes deductible. It is a member-surplus tool, not a substitute for contractor fees. Do not blend ristourne, dividend, and QOLAB cash-out in one instrument.

### Recommended characterisation (to put in the contract)

> QOLAB credits are not shares, not a right to profit as such, and not a negotiable instrument. Cash paid under a distribution round is a **contingent success fee for identified services**. The invoice at cash-out is the consideration. Credits that never cash out lapse or remain as weights with no claim.

---

## Should contributors be members?

**Not required** for the fee to be a cost.

| Approach | Pros | Cons |
| --- | --- | --- |
| Contributors **need not** be members | Clean supplier story; tokens ≠ shares; easier for one-off / foreign contributors | Weaker cooperative identity |
| Contributors **must** be members to earn R | Matches ICA “member participation” | Cash-out looks like surplus; SO dividend cap; admission/KYC overhead |
| **Split (recommended)** | Members (optional) for governance: one member, one vote, modest share. QOLAB credits for work, by contract, **explicitly not** a membership right | Two onboarding paths to explain |

If Refaqt is or aims to be a **CV erkend als sociale onderneming**, keep QOLAB payments **off the share**. “Any patrimonial advantage whatsoever” to shareholders is capped. Paying a member €50,000 on tokens while they hold €100 of shares is exactly the fact pattern that statute is written to catch **if** the payment is treated as an advantage on the shares.

---

## Peer sales of R and U

The current rule (“internal, but contributors can sell to each other”) is the highest-risk sentence in the design.

It tends to create:

1. **A market price** → VAT and income tax at grant (disposal right + ascertainable value).
2. **A tradable claim on future revenue** → FSMA “beleggingsinstrument” / public-offer analysis; if on DLT, **MiCA** (utility token white paper, or worse ART/EMT).
3. **U = 1 euro**, transferable, accepted by others → **e-money** analysis (Directive 2009/110 and Wet 11 maart 2018), even off-chain. MiCA EMT rules need DLT or similar; e-money rules do **not**.
4. Buyers who did **no work** receiving the 10% pool → dividend / investment characterisation.

MiCA Recital 17: a token is “non-transferable” only if it is accepted **only by the issuer** and there is **no technical possibility** to transfer it to anyone else. “Only among contributors” is still transferable.

**Recommendation:** R is non-transferable except (a) back to the treasury, (b) universal succession (death), (c) same beneficial owner (e.g. eenmanszaak → BV). No U-token.

---

## What contract?

Refaqt should not have a single contract type for everyone. Classify the **relationship**, then pick the instrument.

| Relationship in fact | Contract | QOLAB? |
| --- | --- | --- |
| Authority, set hours, integration into organisation (arbeidsrelatiewet: will, organisation of work, organisation of time, hierarchical control) | **Employment contract**. Salary in euro. | Do not replace wages with tokens. |
| Independent professional, own organisation, invoices, can refuse work | **Dienstenovereenkomst** (framework) + SOW/task tickets + **CLA / IP assignment or licence** + QOLAB annex | Yes |
| Occasional unpaid volunteer | Volunteer rules; no remuneration | No cash QOLAB, or you destroy volunteer status |
| Member as such | Membership, statutes, share subscription | Governance only |

Package for the target design:

1. **Framework services agreement** — parties, no employment, deliverables, fees (contingent QOLAB + any cash retainers), liability, termination, governing law Belgium.
2. **QOLAB regulation** (annex) — how weights are earned, non-transferability, distribution rounds, caps, invoice procedure, VAT-exclusive pool, lapse.
3. **IP / CLA** — Refaqt can use and commercialise the work (licence or assignment, consistent with open-hardware policy).
4. **Optional membership** — separate; buying a share does not grant extra R.

Tax clause: each party is responsible for its own taxes and social charges; contributor issues a valid invoice (or reverse-charge invoice) **before** payment; Refaqt does not withhold PIT unless legally required (e.g. if the person is a bedrijfsleider).

Foreign contributors: map place of supply, VIES, reverse charge, and (for US persons) a separate `us-law` review. Default: do not onboard US persons until that is done.

---

## What breaks the “no tax at grant” goal today

| Design choice | Why it hurts |
| --- | --- |
| Bonding curve used as a **euro price** to mint U | Gives R a market value on day one |
| **1 U = 1 euro** | Looks like a par claim / e-money, while the pool formula does not actually pay €1 per U |
| **Peer transfer** of R and U | Disposal + price discovery |
| Immediate C→R conversion described as “reward” | Sounds like payment at grant |
| 10% of **revenue** to anyone holding tokens | Profit-participation / investment narrative, and can exceed profit |
| Unused U “converted back at the old price” | Confirms that a price existed |

The bonding curve as a **mint function for weights** (later contributors get fewer weights per hour) is fine. Using the same curve as an **FX rate into euro** is not.

### Internal contradiction: “1 U = 1 euro” vs the pool formula

The sketch says both:

- 1 U-token is 1 euro, and
- euros received = `pool × U_offered / total_U_offered`.

Those cannot both be true. The second formula always empties the pool onto **offered** U:

- If little U is offered, each U receives **more than** €1.
- If much U is offered, each U receives **less than** €1.

U is then a **pro-rata chip**, not a par claim. Calling it “1 euro” is the worst of both worlds: it looks like e-money or a face-value debt to a regulator, while economically it is just a share of whatever is in the pot. If everyone in a given round converts R→U at the **same** curve price, that price also **cancels** in the pro-rata (`payout_i ∝ R_i`). The U layer then adds legal risk without changing who gets what.

Drop U. Split the pool on weights directly.

---

## Design that hits the four goals with less tax surface

Keep the economics; change the legal object.

```
work (hours or estimated effort) → non-transferable weight W
     W_new = effort × early-bird factor(total W)
when Refaqt has a distributable pool:
     opt-in: offer W into the round
     payout_i = min( pool × W_i / Σ W_offered , remaining personal cap )
     invoice in euro (VAT exclusive) → pay → burn offered W
     unoffered W stays as weight, still no claim
```

No C-token, no U-token, no published euro price for W.

### Early-bird without a price

Use a **weight mint**, not a price:

- Vintage multipliers (year 1 = 2.0×, year 2 = 1.5×, …), or
- Power-law mint: `ΔW = effort / (W_total + 1)^α` with α chosen so early work is clearly advantaged.

Store **effort units**, not euros, on the ledger. A reference hourly rate exists **only inside the cap formula at payout**, not as a grant-time valuation.

### Caps (goal 2) and higher-than-hourly (goal 3)

At payout, each person has a **notional ceiling**:

`lifetime_cap_i = k × Σ (hours_i × reference_rate_i)`

with e.g. `k = 2` or `3`.

- Payouts stop when the cap is reached → **cap**.
- Until then, a successful Refaqt can pay **more than** hours × rate → **higher return**.
- If Refaqt never has a pool, payout is **zero** → tax and VAT stay at zero.

Reference rate: freeze per contribution at the then-published contractor band (or task estimate), used only for the cap. Do not book it as a payable.

### Scale with Refaqt (goal 4) without a 10% revenue cliff

Replace “10% of revenue” with a **waterfall** that cannot insolvent the cooperative:

1. Cash after operating costs, reserves, and a board/GA solvency check.
2. Pool = `min( p% of gross profit or EBITDA , q% of revenue , cash available )`.
3. Board (or GA policy) opens **distribution rounds**; no automatic claim.

`p` and `q` are policy, not a token-implied right against turnover. 10% of revenue is dangerous if margins are thin.

### Reward at the moment of revenue (goal 1)

The euro (and the invoice) exist only in a round funded by actual receipts. Weights earned in lean years still participate later — that is the deferred success fee.

### Implementation defaults (token-engineering + web3)

- **Off-chain ledger** (database). No DLT unless there is a later, counselled reason.
- No public ROI language. Call them **contribution credits / weights**, not coins.
- Treasury and VAT cash-flow live in the finance model (output VAT of contributors is their problem; Refaqt’s input VAT and the extra 21% cash on invoices is Refaqt’s).

---

## Indicative cash-out example (Map B, Belgian self-employed, normal VAT)

Pool allocates **€10,000 VAT-exclusive** to Alice. She is in the 50% PIT band.

| Step | Alice | Refaqt |
| --- | --- | --- |
| Invoice | €10,000 + €2,100 VAT | Pays €12,100 |
| VAT | Remits €2,100 | Deducts €2,100 if entitled |
| Deductible cost | — | €10,000 (VenB 20–25% saved) |
| Social ~20.5% | ~€2,050 (deductible) | — |
| PIT + municipal on ~€7,950 | ~€4,250 | — |
| Alice net of PIT/social | ~€3,700 on this €10,000 | — |

Numbers are rounded illustrations, not a tax computation. An accountant must model the real contributor (company vs natural person, bracket, expenses, reverse charge).

Same €10,000 labelled as a **dividend** to a member: Refaqt **cannot deduct** it, withholds **€3,000**, Alice nets **€7,000**, no VAT. Cheaper for Alice, worse for Refaqt, and likely the **wrong legal box** if the economic cause is work.

---

## Regulatory screen (short)

| Topic | Current design | Target design |
| --- | --- | --- |
| MiCA | If DLT + transferable: at least “other crypto-asset”; U≈euro risks EMT | Off-chain, non-transferable, issuer-only: outside MiCA |
| E-money | U=€1 transferable is the red flag | No par token |
| FSMA / prospectus | Peer market + revenue share | No offer of an investment; credits are a fee formula |
| DAC8 | If a CASP/wallet is used, reporting from 2026 | Avoid public crypto rails |

---

## What to take to humans before launch

1. **Belgian tax lawyer + accountant** — confirm Map B (no taxable event at grant) for the final regulation text.
2. **DVB (advance ruling)** — grant vs payout timing for PIT and VAT; characterisation as fee not dividend.
3. **Counsel on statutes** — tokens ≠ shares; SO dividend cap; GA authority to adopt the regulation.
4. **Employment / social** — contractor vs employee policy; optional ruling of the Administratieve Commissie Arbeidsrelaties for close cases.
5. **NBB/FSMA** only if anyone still wants transferability or a euro-pegged unit.

Until those sign-offs exist, treat this document as a **pre-legal spec**, not a launched scheme.
