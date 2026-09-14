# 2026-09-14 — Investors, the no-freeze bond row, and the two-leg waterfall

**Role(s):** finance, business-dev

**Status:** New path, **open (proposed)** — [capped participating bond](../../token-system-design/paths/capped-participating-bond/README.md), [ADR 2026-09-14](../decisions/2026-09-14_investor-leg-capped-participating-bond.md). Design input for counsel, not a ruling and not an offer.

**Prevention rules applied:** [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md) — nothing here is issued for work; [do not put a euro spot price on contribution credits](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [never write a ceiling as a balance times `(1 + r)`](../mistakes/2026-09-14_cap-as-balance-times-one-plus-r.md); [no multiple on the effort base](../mistakes/2026-09-14_10x-on-the-effort-base.md). New rule out of this pass: [a second instrument must not publish the comparable the first is designed not to have](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).

## What happened

Asked how to add **investors**, and then the **combination of contributor and investor**, to the token system. The proposal was to mirror the option-2 contributor cap: an investor buys in for `I_i(n)`, is paid `d_i(n)` with cumulative `D_i(n)`, and is bounded by `U`, `O`, `cap`, `rem` rows with the **same `k` and `r`** as contributors. The yearly money going to contributors should then be proportional to `Σ rem_i / (Σ rem_i + Σ rem^S_i)`.

Three rounds. The first pass converted the instrument from shares to debt; the second removed the freeze and settled governance; the third is what is written up.

---

## 1. A per-investor cap cannot ride on a share

The proposal said "buy shares" and "dividend payments". A dividend must be **equal per share inside a *soort***, so paying one holder and not another is not writable. Three routes out, all rejected:

| Route | Verdict |
| --- | --- |
| Cap per investor on a single class | Not writable. The unequal treatment *is* a class difference |
| One class per subscription vintage | Works, and costs 10+ live classes, a class vote on every amendment (art. 6:87 WVV), and a register tracking vintage. Already priced and rejected for the sunset in [2026-09-11 §5](2026-09-11_cheap-share-ab-classes-sunset.md) |
| A share amortising to nothing | Forced redemption at par after a bounded stream is the "the share was never equity" fact from [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md); and a share with neither profit nor liquidation right runs at art. 4:2 |

A **debt instrument** gives each investor their own position, exactly as each contributor has their own row, and the cap is then an ordinary contract term. That is the whole reason for the switch.

## 2. Two things that fall out in the design's favour

**The VenB wedge disappears.** With a dividend leg, matching a target ratio means solving `F + Dv/(1−t) ≤ W`, because a dividend comes out of post-VenB profit and a fee is a deductible cost. A deductible uplift makes both legs pre-tax outflows, so the split is met **exactly** at leg level. The user's "more or less met" turns out to be achievable exactly; the only approximation left is per-person clipping at caps, which a carry ledger absorbs.

**The accountant instruction stops contradicting itself.** [annex clause 27](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md) says the contributor ceiling must never be booked as a liability — the clause that decides the characterisation in practice. A bond principal **must** be booked. Those two instructions are only coherent while the two instruments are separately named, which is independently required for the reason in §5.

## 3. The freeze does not belong on the investor leg

Carrying the contributor row over unchanged means `U^I = max(0, I(n−1) − D(n))`, which reaches zero once payments cover the principal, and the uplift then stops. That was rejected: principal being repaid should not stop the cap growing.

The fix is the **burn applied to a position instead of to weights**. Accrue simple interest on outstanding principal, and haircut the whole position proportionally on payment:

```
accrual_i(n) = min( r_I · U^I_i(n−1),  (k_I − 1)·I_i(n) − Ocum^I_i(n−1) )
Ocum^I_i(n)  = Ocum^I_i(n−1) + accrual_i(n)
O^I_i(n)     = O^I_i(n−1)    + accrual_i(n)
rem^I_i(n)   = U^I_i(n) + O^I_i(n)
h            = ( rem^I_i(n) − d_i(n) ) / rem^I_i(n)
U^I_i ← U^I_i · h        O^I_i ← O^I_i · h
```

Nothing freezes, and it cannot run away either, because each payment shrinks the accrual base. **The lid survives exactly**: every euro paid comes out of `U^I + O^I` and the only things ever added are `I` and `Ocum^I`, so `D = I + Ocum^I ≤ k_I · I` over the life of the instrument. Confirmed to the euro in the worked run below.

### 3.1 The lid is not the freeze

Worth writing down, because conflating them is how the design loses its bound:

| | Freeze | Lid |
| --- | --- | --- |
| Stops | the **accrual**, when the thing at risk stops being at risk | the **lifetime total**, at `k ×` the base |
| Contributor | yes (`U = 0` after the work is paid for) | yes (`cap ≤ k · E`) |
| Investor | **no** | yes (`D ≤ k_I · I`) |

Dropping the lid too would make the instrument an unbounded claim on all future surplus — the hidden-dividend shape from [option-2 §10](../../token-system-design/paths/option-2-contingent-fee/README.md), and the pattern [ADR 2026-09-14](../decisions/2026-09-14_simplified-cap-one-row.md) refused.

### 3.2 One principle, two consequences

[Option-2 §5.2 point 3](../../token-system-design/paths/option-2-contingent-fee/README.md) calls the freeze *"the single strongest fact in the set"*, so the asymmetry needs a reason rather than an exception:

> Work stops being at risk once it has been paid for. Money stays at risk for as long as it is still in the company.

Both legs accrue only while the thing at risk is at risk.

### 3.3 Worked numbers

`r_I = 0.25`, `k_I = 3`, €50,000 advanced in year 1. Never paid: the uplift accrues €12,500/yr from year 2, reaches the lid in year 9 at 3.00×, flat thereafter. Paid €12,000/yr from year 3: the position closes in year 13 having paid €121,300 = €50,000 principal + €71,300 uplift = **2.43×**, under the lid. A realistic payment path lands well below the lid, which matters for §5.

## 4. The split, and the two-leg run

```
θ(n) = Σ rem^C_i(n) / ( Σ rem^C_i(n) + Σ rem^I_i(n) )
P^C_t = θ(n) · P_t        P^I_t = (1 − θ(n)) · P_t
```

`P_t` keeps its existing waterfall, computed before either leg. Re-pass within a leg only; anything neither leg absorbs stays with the CV; deviations carried and corrected next year.

Both legs together, `r = r_I = 0.25`, `k = k_I = 3`, €10,000 of effort accepted in each of years 1–3, €50,000 advanced in year 1, `P_t` = 0, 0, 20k, 30k, then 40k/yr:

| Year | `rem^C` | `rem^I` | `θ` | `P^C_t` | `P^I_t` | To reserves |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 3 | 37,500 | 75,000 | 0.333 | 6,667 | 13,333 | 0 |
| 4 | 36,667 | 71,944 | 0.338 | 10,128 | 19,872 | 0 |
| 5 | 29,840 | 59,511 | 0.334 | 13,359 | 26,641 | 0 |
| 6 | 16,482 | 36,979 | 0.308 | 12,332 | 27,668 | 0 |
| 7 | 4,150 | 10,345 | 0.286 | 4,150 | 10,345 | 25,505 |
| 8+ | 0 | 0 | — | 0 | 0 | 40,000 |

Contributors end at 1.55× their documented effort, the investor at 1.96× the amount advanced, both against a 3.00× lid, and `D = I + Ocum^I` holds to the euro. Two things to read off it:

- **`θ` is met exactly** while both legs have room — year 4 pays 10,128 / 30,000 = 0.338.
- **`θ` drifts down** across the run, because the contributor leg's accrual freezes while the investor's does not. That is the design working, and it is the number to watch when `r_I` is set.
- From year 8 the whole pool is the CV's. **Once both legs are capped the residual belongs to the mission** — the endpoint, and the strongest non-tax rationale the structure has.

## 5. `k_I`: the deduction is what constrains it, not the base

Asked directly whether `k = 10` is defensible. Two different answers.

**Contributor `k = 10`: no, and already decided.** [ADR 2026-09-14 two bases](../decisions/2026-09-14_two-bases-10x-off-effort.md) puts option 2 at or near 1× because `k × hours × frozen band` hands the administration the comparable. Fallback B keeps it documented, needing evidenced `P_t = 0` years and rows that lapsed unpaid, and expecting the number back as a condition. Not reopened here.

**Investor `k_I`: different base, and then a catch.** On capital at risk there is no wage comparable, and a 10× on a successful early investment is an unremarkable outcome nobody computes an implied rate on. But the moment the CV **deducts** the uplift, the comparable stops being a venture return and becomes a lending rate: art. 55 WIB 92 (deductible only up to market rate) and art. 18, 4° (interest requalified into dividends above market rate, for interest to directors or shareholders).

> The deductibility that makes `θ` exact is the same thing that rate-caps `k_I`.

That is the mirror of the contributor problem and it belongs on the record rather than being discovered later. Three notes:

- **Shape beats the lid.** At `r_I = 0.25` the lid needs `(k_I − 1)/r_I` years of total non-payment to bite — 8 years at `k_I = 3`, **36** at `k_I = 10`. Realistic paths land far below it (§3.3). Art. 55 tests the effective rate paid, not the lid.
- **If a real 10× for capital is wanted**, the consistent move is the one already made for labour: **two bases for capital** — a modest deductible `k_I` on the bond plus genuinely uncapped equity on the [cash-shares path](../../token-system-design/paths/cash-shares-residual/README.md). Open, not decided.
- `k_I = 10` is flatly incompatible with art. 8:5 WVV recognition *als sociale onderneming* (~6% cap), which [mission.md](../mission.md) already flags. A capped return moves the design **toward** that regime.

## 6. Uniform terms and no individual veto changed the sub-route

The requirement: same terms for everyone, changes by one person one vote, no single holder able to block. Bilateral loan contracts fail this at the first step — amending a contract needs that counterparty's consent, so **every lender would hold a veto over their own terms**. The collective mechanism has to be inside the instrument at signing.

- **One class, one set of [Loan Regulations](../../token-system-design/paths/capped-participating-bond/loan-regulations.md).** Only the amount and the year vary per holder, mirroring the contributor side where the annex is one standard document and only hours vary.
- A **bond issue carries a holders' meeting** able to bind dissenters by qualified majority. Counsel: arts. 7:170 ff. WVV are the NV machinery; availability, majorities and reserved matters for a CV bond under art. 6:19 need confirming.
- **One person one vote lands in two different rooms.** For the general assembly it is written into the statutes (the WVV default attaches votes to shares). For the holders' meeting it is harder: statutory bondholder voting is normally **by nominal amount**, so a large holder dominates — a different failure from a veto, but still one. If per-head voting cannot be written into the issue conditions, a **concentration cap** bounds it directly, and is worth adopting either way.
- **Future-accrual-only** is what makes the absence of a veto fair rather than expropriatory, and is probably also what makes a majority-amendment clause enforceable. Mirror of [annex clause 13](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md).

**The objection an investor will actually raise** — contributors are the members, so contributors vote on my terms — is the mirror of [2026-09-11 §4.3](2026-09-11_cheap-share-ab-classes-sunset.md). The answer is that **`θ` is formulaic, not discretionary**: the board decides how much is distributed, and nobody votes on the split. That is now `θ`'s main governance virtue.

## 7. Contributor and investor together

Two positions, no netting, and the person appears in both sums. The rules that matter are anti-abuse rather than arithmetic: what a person may advance must never be a function of `c`, `p`, hours or their contributor row, and allocation of `P^C_t` must never be a function of their advance; cash in must be **real money**, because netting an advance against something the CV owes is the *inbreng van een schuldvordering* problem from [2026-09-11 §2](2026-09-11_cheap-share-ab-classes-sunset.md) in debt clothing; and no pre-agreed reinvestment, which would rebuild the labour quota with an extra step.

One asymmetry worth stating: **exclusion for cause on the contributor leg must not touch the bond.** A ceiling that was never a receivable can lapse; money that was actually advanced cannot be confiscated.

## 8. The new prevention rule

Option-2 §5.2 rests on *"there is no principal — the contributor supplied work, not money."* On this leg there **is** principal, and the accrual is simple interest on a declining balance. That is correct here. The danger runs the other way: an investor must be told the return terms, and an FSMA *informatienota* compels the disclosure, so publishing *the same named parameter* would hand the administration the proof that `r` is a capital return rate on the contributor leg too.

This is the same shape as [2026-09-11 §4.1](2026-09-11_cheap-share-ab-classes-sunset.md), where a second share class published the euro price of an hour that the first class was designed not to have. Two instances make it a rule: [2026-09-14 mistake](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md). The fix adopted is **separate names, same values allowed**: `r_I` and `k_I` never appear in a document with `r` and `k`.

It also forces an amendment to a binding constraint. "Never publish `r`" cannot survive contact with an investor, so the path map gains a **second** carve-out beside the contributor-statement one from [ADR 2026-09-14 one-row cap](../decisions/2026-09-14_simplified-cap-one-row.md): an offering document may state `r_I`, `k_I` and the cap, and nothing about the contributor leg.

## Decisions

Recorded as [ADR 2026-09-14 investor leg](../decisions/2026-09-14_investor-leg-capped-participating-bond.md) (Proposed): subordinated participating bond; the no-freeze row with the lid intact; `θ` as a formulaic split; `r_I` / `k_I` as separate parameters; uniform terms with majority amendment, future-accrual-only, and a concentration cap; the offering-document carve-out; and DVB items **(t)** and **(u)**.

## Open Questions

- The values of `r_I` and `k_I`, and whether the comparable exercise puts them at the same numbers as `r` and `k` or apart.
- Whether a real 10× for capital is wanted, and so whether **two bases for capital** is pursued alongside the bond.
- Counsel: holders'-meeting machinery for a CV bond under art. 6:19 — availability, majorities, reserved matters, and whether per-head voting can be written into the issue conditions.
- Counsel: enforceability of majority amendment where it reduces an existing entitlement, with future-accrual-only as the protection.
- Counsel: the article and permitted deviation for one-member-one-vote in the statutes.
- Counsel / FSMA: *informatienota* or prospectus scope for a bond offered beyond members, and whether a recognised-cooperative exemption applies.
- Whether the concentration cap is adopted, and at what percentage; the de-minimis close-out threshold.
- Whether `P_t` is computed before or after the prior year's carry-ledger correction.
- Whether a sunset applies on this leg at all — there is no freeze for it to reach, so it would have to stop the accrual outright.

## Next Steps

- Do not offer anyone a bond, a rate, or a multiple. Nothing here is accepted and the FSMA question is open.
- Counsel on the six items above before any issue conditions or statutes are drafted; accountant on the clause 23 instruction (principal booked, uplift not accrued).
- Run the comparable exercise for `r_I` / `k_I` before either number is proposed to the general assembly.
- File **(t)** and **(u)** with whichever capital base is pursued; **(q)** goes with them.

## Sources checked

Re-used from this repo rather than re-researched: class rights and amendment (art. 6:87 WVV) and the *soort*-per-vintage finding, the *scheidingsaandeel* default, leonine-clause exposure (art. 4:2), VVPRbis *voorkeurrecht* (art. 269 §2 WIB 92), and the FSMA *informatienota* threshold — all from the [2026-09-11 log](2026-09-11_cheap-share-ab-classes-sunset.md) and its sources. Rates and the option-1 / option-2 comparison from [belgian-tax-and-company-law.md §4](../../token-system-design/analysis/belgian-tax-and-company-law.md). Art. 55, art. 18, 4° and art. 198 §1, 11° WIB 92 are named here as the tests that apply and are **not** verified in this pass — they are counsel items, listed in [dvb-questions.md](../../token-system-design/analysis/dvb-questions.md). Arts. 7:170 ff. WVV are cited as the NV bondholders'-meeting model; whether they reach a CV bond issue is explicitly unverified.
