# 2026-09-10 — Tokens not shares, to avoid the bedrijfsrevisor (discussion)

**Role(s):** finance, business-dev

**Status:** Open exploration. Not accepted. Does not replace the option-2 pass. No ADR. Design input for counsel, not a ruling.

**Prevention rules applied:** [do not put a euro spot price on certificates](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not combine a cheap grant value with a steep curve](../mistakes/2026-09-07_steep-curve-low-grant.md). Token-engineering: labels do not take compensation outside VAT or income tax; facts beat labels.

## What happened

Asked whether contributors can be paid with **tokens instead of shares**, so each contribution does not need a **bedrijfsrevisor** and is not **inbreng in nijverheid**. VAT and tax if the tokens have monetary value is acceptable for this fork. Then compared phantom shares, revenue-share and profit-share tokens, asked whether a BV or CV can issue those (or only an NV), whether returns must stay **arm’s length**, and whether a **warrant** exercised in cash later would work — including cashless exercise and a sale back to Refaqt. Later asked how to keep a **10× upside** if the CV accepts **no deduction**, **VenB first**, and **30% WHT**, while having the administration **not look at arm’s length**, still without a revisor (see §7).

### 1. Tokens instead of shares skip the inbreng-revisor

The bedrijfsrevisor attaches to **issuing shares against a non-cash / labour contribution**, not to “having a ledger.”

- **Triggers:** *inbreng in natura*; *inbreng in nijverheid* (art. 1:8 WVV: work for shares, which must be valued); later **conversion** of a work-token or receivable into shares (inbreng of a *schuldvordering*).
- **Does not trigger:** a small **cash** governance share (*inbreng in geld*); paying a contractor (invoice, voucher, bonus, phantom); an internal credit that is **contractually not a share**.

That is already the company-law reason for option 2. The extra option-2 machinery (no euro par, contingent invoice, effort cap, `p` burn) is mostly about **deferring VAT/tax until cash-out**. If tax at grant is accepted, a simpler non-share token can still skip the revisor.

To stay out of share-land the token must not look like a *soort aandeel*: no vote via the token, no residual claim on NAV / liquidation, no peer market, cash-out is an invoice / contractual sum, **never convert** balances into shares. Statutes already say credits are not parts/shares ([ADR 2026-09-02](../decisions/2026-09-02_tax-aware-contribution-credits.md)). If those facts slip, FPS or a court can still say the real contribution was *inbreng in nijverheid*.

There is no third tax box. Priced tokens for labour are a **fee** (VAT 21% + professional income / VenB), not a dividend. You cannot have both “not a dividend” and “not a fee” ([token-system.md](../../token-system-design/token-system.md)).

### 2. Phantom shares vs revenue-share vs profit-share tokens

Same legal box if they stay contracts (not shares → no inbreng-revisor) and usually the same tax box (fee / bonus). They differ in **what the euro amount is indexed to**.

| | Phantom shares / SAR | Revenue- or profit-share tokens |
| --- | --- | --- |
| Object | **Stock:** company value (NAV, round, exit) | **Flow:** this period’s revenue or profit / GA pool `P_t` |
| When cash appears | Valuation event, vesting, exit; sometimes a yearly mark | Each period there is a pool |
| Needs a share **price** | Yes — a CV often has none | No |
| Closest QOLAB object | Not in the live spec | Option 2 / invoiced royalty |

Live option 2 is already the flow family: weights `p` split a pool. Phantom copies **ownership value**. A GA that “sets” a share price is not a market.

A perpetual profit-share that also claims leftover assets starts to look like phantom equity. A phantom that only pays a dividend equivalent starts to look like a profit-share token.

### 3. Can a BV or CV issue profit-share tokens? (not only an NV)

Classic **winstbewijzen** (arts. 7:58–7:59 WVV) are an **NV** security: they do not represent capital. Labour cannot be paid with capital-representing NV shares (art. 7:6).

A **CV cannot** issue them. Art. 6:19 WVV: only registered **voting shares** and **bonds**. No *winstbewijzen*, no non-voting shares, no certification. Different profit rights are still possible as **share classes** (arts. 6:40, 6:46), but a share may only be issued **in ruil voor een inbreng** (art. 6:39) — work-for-shares is then *inbreng* again.

A **BV** is the messy middle. Art. 5:18: all securities not forbidden (no *numerus clausus*). Book 5 has no *winstbewijzen* chapter; the *memorie* said they were unnecessary (no capital; shares can already be issued for *inbreng in nijverheid*). Doctrine is split. Even if allowed, **voting rights may only attach to shares** (art. 5:41). Practical advice: use a **share class**, not that name.

Three layers:

1. Classic *winstbewijzen* — NV; disputed/redundant in a BV; **no** in a CV.
2. Share class with extra profit rights — BV, CV, NV. That is option 1. Issued for work → auditor + labour-quota facts.
3. **Contractual** profit-share / revenue-share / phantom — any legal person, including BV and CV. Not a security. Fee, not dividend.

Revenue-share is **not** the only BV/CV option. A BV/CV cannot reliably issue NV-style *winstbewijzen* so contributors get a statutory profit right without being shareholders and without a fee.

### 4. Arm’s length

For all three contract types, the money is still **pay for work**. Art. 49 WIB 92 (not excessive), art. 26 (abnormal advantage to a related party), *vennootschapsbelang*. The comparable is the market price of the **service**, including how independents price delay and non-payment — not a “fair ROI on phantom equity.”

The live effort cap is that brake: an invoice ceiling on documented effort, not a yield on `p` ([vintage-pools.md](../../token-system-design/vintage-pools.md); [ADR 2026-09-04](../decisions/2026-09-04_fee-cap-not-unit-price.md)).

If lifetime or expected payout ≈ hours × frozen contractor band, that **is** the arm’s length quantum. Paying less because the fee is contingent is still arm’s length. Paying more needs a real *ex ante* success-fee reason (risk of earning nothing). A `k×` open on day one with a forecasted fat pool is the [gold-rush](../mistakes/2026-09-03_immediate-multiple-gold-rush.md) pattern.

Use “what they would have invoiced” as an **internal benchmark**, not as contract wording that sounds like an unissued invoice (VAT when the service was performed). Uncapped phantom or revenue % can leave that band even if the *grant* was meant to equal the invoice.

### 5. Worked phantom: 4,568 `p`, GA price to €50, put to Refaqt

Sketch: `p` are phantom shares; 1 `p` = 1 phantom; phantom price = a CV share-class price. Contractor does **€5,000** of work (50 h × €100). Issue **5,000 `c`** at **1 `c` = €1**, mint **4,568 `p`**, so grant “price” = €5,000 / 4,568 ≈ **€1.09 / `p`**. Later the GA sets the share price (and `p`) to **€50**. Contributor sells **500 `p`** for **€25,000**, then more to Refaqt. Variant: at grant they could already put the whole bag to Refaqt for **€5,000**.

If all 4,568 `p` cash at €50: **€228,400** (~**46×** the work).

The grant of 4,568 phantoms then worth €5,000 can be a **cost** (fee in kind) and arm’s length *at grant*. `1 c = €1` plus `value = work / Δp` is a grant-time unit FX (`w = dc/dp`). A put at grant for €5,000 makes the right **vested, priced, and disposable** → VAT and professional income on ~€5,000 **now**; option-2 deferral is gone.

The ride to €50 on a **GA-set** price with an **issuer put** is a second, much larger benefit. A GA number is not a market print. Then selling 500 `p` for €25,000 (and potentially €228k) is a discretionary bonus / related-party advantage, not “the share market moved.” Returns should stay within an **effort cap**. Bonding-curve extra units *and* price appreciation is the [2026-09-07 dead-end](2026-09-07_bonding-curve-shares-dead-end.md). If `p` must track a share price, the honest mint is `Δp = fee / current_share_price`.

**Cost vs dividend vs real buyback**

- True phantom (no vote, not on the share register): grant ≈ cost of €5,000; later cash at €50 is **more fee** if it stays compensation, or **abnormal advantage / disguised distribution** if out of line. Cash-settled phantom is not a tax-free private capital gain.
- Recharacterised as hidden shares: no deduction, possible 30% WHT, possible VAT + PIT, *inbreng* / revisor you were avoiding.
- **Real CV share buyback / uittreding:** not a deductible cost. Surplus over fiscal paid-in capital is generally a **dividend**. Typical *uittreding* pays back the *inbreng*, not NAV. Paying NAV per share is how a labour class drains the CV ([2026-09-08 log](2026-09-08_option-1-tenth-vs-ten-euro-shares.md)).

Do not use share-buyback mechanics if you want option-2 cost treatment.

### 6. Warrants: exercise in cash, net €15,000 with Refaqt?

Sketch: warrant “for €5,000” (VAT and tax at grant?), later buy for €5,000 and sell at €20,000. Is a revisor needed at grant? Must they have €5,000 cash, or pay Refaqt and sell to Refaqt in one go (net **€15,000**)? Invoice + VAT on that €15,000? VenB on €15,000 unless they own **>10%**?

Two objects: **inschrijvingsrechten** (WVV security: new shares from the company) vs **aandelenoptie** (contract: existing shares from a grantor).

- **BV / NV** may issue *inschrijvingsrechten* (arts. 5:55–5:60). A **CV cannot** (art. 6:19). For a CV: contractual option on existing shares, convert to a BV, or a carefully drafted contract to issue new CV shares for cash later.
- Strike = current value = **ATM**. Tax at grant is on the **option**, not the €5,000 notional. **Optiewet** (26 March 1999), natural person, written accept within **60 days**: lump sum usually **~18% of underlying share value** (≈ €900 on €5,000), plus 1% per extra year of term beyond five. Miss the 60 days → typically the **full €15,000 spread** as professional income at exercise. Halved 9% often **lost** if granted to the zaakvoerder of a management BV (circular 2017/C/21). Optiewet does **not** apply to a contributor **BV** as beneficiary. Cash-settled options are **outside** Optiewet.
- **VAT at grant:** contractor, yes, on option FMV / forfait. Employee wages are outside VAT. **Social:** zelfstandigen pay on the benefit; employees can be outside RSZ under Optiewet.
- **Bedrijfsrevisor at grant:** not the *inbreng in nijverheid* report (no shares yet). Often a **revisor or accountant valuation** of unlisted shares for Optiewet art. 43. Inbreng-revisor returns if exercise is **set-off of a receivable**, not real cash. Exercise for **cash** = *inbreng in geld* → no inbreng-revisor.
- **€5,000 cash:** the company must receive €5,000 as cash *inbreng*. It can come from a simultaneous **third-party** sale (escrow: buyer pays €20,000; €5,000 to Refaqt; €15,000 to the contributor). **Netting with Refaqt** is *inkoop van eigen aandelen*: distribution tests, **not deductible**, surplus over fiscal capital generally a **dividend** (30% WHT for a natural person). That circular set-off also looks like cash settlement or inbreng of a claim.
- **€15,000 invoice / VAT:** no if they sell **shares to a third party** (VAT-exempt securities). **Yes** if Refaqt just pays the spread (extra consideration for the work). Refaqt does **not** deduct the €15,000 on a genuine equity-settled warrant (dilution, not a wage cost).
- **VenB / 10%:** a contributor **BV** is outside the 2026 10% *meerwaardebelasting* (that is personenbelasting). Share gains are VenB unless **DBI**: **10% or acquisition value ≥ €2.5 million**, **and 1 year** holding, and subject-to-tax. Same-day sale fails the year. €5,000 of shares is not €2.5 million and will almost never be 10% of Refaqt → ordinary VenB (20% SME / 25%) on the €15,000. A **natural person**: 10% *meerwaardebelasting* from 1 January 2026 (category C, yearly exemption in the order of €10,000), or professional PIT + social if FPS keep it as pay for work. The **20%** stake is the *aanmerkelijk belang* scale, not 10%.

The warrant only does the intended job if someone **other than Refaqt** pays the €20,000. Then the €15,000 is equity upside funded by a buyer. That is a different product from option 2: no deduction of the upside at Refaqt; real shares; dilution; *voorkeurrecht*; FSMA if offered broadly; Optiewet valuation of an unlisted company. It does not scale to every contribution.

### 7. 10× of contribution, VenB + 30% WHT, no arm’s length, still no revisor

Asked how to keep a **larger upside (10× the contribution)** if the CV **accepts that the payout may not be deductible**, that **VenB is paid first**, and that payment is preceded by **30% WHT** — and, at the same time, make it so the administration **does not look at arm’s length**, while still **avoiding the bedrijfsrevisor**.

**The combination does not exist on one labour-minted instrument.** “10× this person’s contribution” is a labour price. Arm’s length is how Belgian tax prices labour. Choosing not to deduct, paying VenB first, and withholding 30% does not turn that formula into a capital return. That is the same prevention rule as [cheap-share labour-quota dividends](../mistakes/2026-09-04_cheap-share-euro-par.md): share *count* or token *payout* that tracks work stays a fee story. There is still no third tax box ([§1](#1-tokens-instead-of-shares-skip-the-inbreng-revisor)).

#### What “don’t look at arm’s length” actually requires

FPS apply an arm’s-length / excess test when the payment is **pay for work**:

- Art. 49 WIB 92 if you deduct (not excessive professional expense).
- Art. 26 WIB 92 (abnormal or benevolent advantage) even if you do **not** deduct.
- Disguised remuneration of a member, plus VAT and professional income on the recipient.

They generally do **not** ask “is this too much for 50 hours?” of a **pro-rata dividend on shares acquired as capital**. A company may distribute all distributable profit. The tests are then WVV net-asset / liquidity, a GA decision, and “is this really a return on shares?”

The administration stops treating the **amount** as a service price only if the cash is a **residual claim on capital**, allocated by **shareholding** (or a real NV profit security), not by contribution points `p` or hours.

That is the opposite of “10× the contribution.” If the payout is still `k × documented effort`, you have told them the comparable: hours × band. Then `k = 10` is DVB item **(p)** — a success-fee bound they can trim — not a dividend they ignore ([dvb-questions.md](../../token-system-design/dvb-questions.md); [cap-opening log](2026-09-10_pt-distribution-and-cap-opening.md)).

#### Not deducting does not buy a free pass

If you book a non-deductible contractual payout to members, you can still get VenB (no deduction) **and** 30% WHT if they call it a hidden dividend **and** VAT + PIT/social if they call it a fee **and**, in a bad identification case, art. 219 (geheime commissielonen). You cannot elect “only VenB + 30%.” Characterisation is facts, not a booking choice.

Option 1 (dividend) is: after-tax profit → GA distribution → 30% *roerende voorheffing*, not deductible, no VAT if it **holds**. That box needs a **share** (or a real profit security). A CV share may only be issued **in ruil voor een inbreng** (art. 6:39). Work-for-shares is *inbreng* again → revisor + valuation.

If instead you keep a **contract** and merely **withhold 30%** and refuse the deduction, you have option-2 facts with option-1 tax. Allocation by points is still the smoking gun that the cause is labour. Ticket price and “we won’t deduct” do not fix the quota ([2026-09-08 log](2026-09-08_option-1-tenth-vs-ten-euro-shares.md)).

*Werkende vennoot* case law helps only when profit is a return on **capital at risk** in a joint enterprise, not a points printer on a trivial cash share.

#### Revisor (unchanged from §1)

| Action | Revisor? |
| --- | --- |
| Small **cash** membership share (*inbreng in geld*) | No |
| Contractor invoice, phantom, revenue-share **contract**, bonus | No |
| Shares (or conversion of a token / receivable into shares) for **work** | Yes |
| Exercise of a warrant / new shares for **real cash** | No (cash *inbreng*) |
| Same exercise **set off** against a claim on Refaqt, or cashless sale **to** Refaqt | Looks like inbreng of a claim or *inkoop van eigen aandelen* — revisor / distribution risk returns |

A CV still cannot issue NV-style *winstbewijzen* or *inschrijvingsrechten* (art. 6:19). Contractual profit-share tokens are available, but they are **fees**, so arm’s length stays ([§3](#3-can-a-bv-or-cv-issue-profit-share-tokens-not-only-an-nv), [§4](#4-arms-length)).

#### Structures that can actually work

**A. Two instruments (the only clean way to keep both goals).** Labour stays off the share register: dienstenovereenkomst, contingent invoice, effort near **1×** (or a DVB-blessed wait-dependent cap). That is option 2. Deductible if it holds. Arm’s length is expected and bounded. No revisor.

Upside is a **separate capital claim** that does not scale with this week’s hours:

- Everyone who should share residual profit **buys cash shares** (same class, or a statutory labour *class* that is **not** `f(p)` — e.g. one share per contributing member, or a fixed split with the investor class, as left open on [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md)).
- 10× appears if the **company** grows and dividends / NAV grow, like ordinary startup equity — 10× of **paid-in capital or company value**, not 10× of hours.
- Payment: VenB first, 30% WHT, not deductible.
- FPS look at affectio / capital at risk / loss absorption, not at art. 49 on the dividend quantum.

Do not mint extra shares from `p`. Do not convert `p` into shares later. Do not put an issuer at a GA-set “share price.” Those bring back labour quota, *inbreng*, or a discretionary bonus ([§5](#5-worked-phantom-4568-p-ga-price-to-50-put-to-refaqt)).

This matches the live design rule: membership share for voting; credits are not parts; do not mix dividend and fee on the **same** instrument ([ADR 2026-09-02](../decisions/2026-09-02_tax-aware-contribution-credits.md)).

**B. NV *winstbewijzen* (only if you leave the CV form for this vehicle).** Classic *winstbewijzen* (arts. 7:58–7:59) are an **NV** security that does not represent capital. Distributions are usually dividends (VenB + 30%, not deductible). They are **not** a CV tool.

They help the revisor story only if they are **not** issued as pay for this contribution (and not as conversion of a work receivable). If the number of *winstbewijzen* is still `f(p)`, you have the same quota. Grant of a real security for work is often taxed **at grant** on FMV. Doctrine on a BV substitute is split; voting still cannot sit on a non-share. Different product from option 2: NV (or conversion), FSMA hygiene if offered broadly, counsel.

**C. Warrant / option, cash in, third-party cash out.** Already [§6](#6-warrants-exercise-in-cash-net-15000-with-refaqt): the warrant only does equity-upside work if **someone other than Refaqt** pays the exit price. Cash exercise = *inbreng in geld* → no inbreng-revisor. Netting with Refaqt is a buyback / fee. A CV cannot issue *inschrijvingsrechten*. Does not scale to every contribution and still has grant-time valuation. It does **not** make a 10× labour token “not arm’s length.”

**D. Live option 2 with gated 10× (arm’s length stays).** The [2026-09-10 cap-opening path](2026-09-10_pt-distribution-and-cap-opening.md) — lots, **1× in the first unpaid year**, then open toward **10× after ~10 unpaid years**, freeze when that lot’s 1× is paid — is how you argue 10× **as a success fee**. DVB **(p)** is exactly “is `k = 10` still a fee?” You **want** them to look at arm’s length; that is how the deduction survives.

That path is the opposite of “accept no deduction and 30% WHT.” If you need 10× **even when they were paid in year 2**, the same log already says that is **shares**, not a higher fee cap.

#### What not to do

- A puttable phantom at a GA-set price so 4,568 `p` become €228k. Grant ≈ invoice can be a cost; the later multiple is a discretionary bonus / related-party advantage. A GA number is not a market.
- Cheap or tenth-euro shares with a `p` quota, with or without burn. Same if there are no investors yet, and same if the quota sits only in a side ledger “until we put it on paper” — [2026-09-10](2026-09-10_no-investors-euro-shares.md).
- Booking a contractual profit-share as a non-deductible “dividend” so art. 49 “does not apply.” Art. 26 and recharacterisation still do.
- Cashless warrant exercise against an *inkoop* by Refaqt.
- Promising 10× or “beats ETFs” in the regulation.

#### Practical target for counsel / DVB

Ask for **two boxes**, not one:

1. **Credits `p`:** contingent success fee; no shares; no conversion; no revisor; arm’s length via a documented effort ceiling (file **(a)–(d)**, **(h)–(j)**, **(p)** if you keep a high `k`).
2. **Residual 10×-shaped upside:** cash-issued shares (or, only if you change form, NV *winstbewijzen*) whose **count is not** `f(p)`; distributions are real dividends; VenB + 30% WHT; no art. 49 on the dividend amount.

If the political goal is “contributors who work more should get more of the 10×,” that **is** the labour quota. Then you stay in option 2 and you **do** invite the arm’s-length discussion — the gated 10× path is the honest version of that. You cannot have that quota, skip the revisor, skip arm’s length, and keep a clean 30% dividend.

## Decisions

None. Sketch stays **open**. Not an ADR. Does not replace option 2. Does not revive cheap-share or bonding-curve shares. Does not unpark vintages. Does not accept a labour-minted 10× as a dividend that FPS will not arm’s-length.

Working conclusions (still for counsel):

- Avoiding the inbreng-revisor = **do not issue (or convert into) shares for the work**. Keep a small cash membership share for voting.
- Phantom / revenue-share / profit-share tokens are available to a **BV and a CV as contracts**. Classic *winstbewijzen* are not a CV tool and are a poor BV substitute for a share class.
- Arm’s length still applies to any **labour-priced** token; an effort cap still belongs unless a real third-party market prices the instrument.
- A GA-set phantom price plus an issuer put is not uncapped equity. Grant ≈ invoice can be a cost; the later multiple is the problem.
- Warrants are a **BV/NV** (or contractual-option) path. Cashless sale **to Refaqt** is a buyback / fee, not a clean share gain.
- **VenB first + 30% WHT + no deduction does not remove arm’s length** from a payout sized as `k × contribution`. That formula stays a fee (or a labour-quota dividend that recharacterises). The administration ignores the service-price test only on a **residual claim on capital** allocated by shareholding, not by `p`.
- Clean split: **option 2** for labour (revisor off; arm’s length expected; deduction if it holds) **beside** cash-issued shares for residual upside (VenB + 30% WHT; no art. 49 on the dividend quantum; 10× of company value, not of hours). Do not mix those boxes on the same instrument.
- Gated option-2 10× after a long **unpaid** wait ([cap-opening log](2026-09-10_pt-distribution-and-cap-opening.md), DVB **(p)**) is the path that *invites* arm’s length so the deduction can survive. It is not the “don’t look” path.

## Open Questions

- Counsel: confirm art. 6:19 for the CV; that QOLAB credits stay off the *effecten* registers; that balances will not convert into shares.
- Whether a priced phantom/revenue/profit-share (tax at grant accepted) is worth a separate spec vs simpler option 2.
- DVB: grant-time VAT/PIT on a puttable phantom; fee vs disguised distribution when a member cashes above documented effort; Optiewet vs contractor VAT if warrants are used.
- If warrants: BV vs contractual option on a CV; who the third-party buyer is at exit; pool size / *voorkeurrecht*.
- How any of this sits next to live option 2 (`P_t`, effort cap, nested mint, project-as-contractor) — replace, sit beside, or drop.
- Whether a **statutory profit split** between a membership class that is **not** `f(p)` (e.g. one cash share per contributing member, or a fixed % vs the investor class) is worth a separate option-1 sketch for the residual box.
- Whether an NV vehicle (or conversion) for *winstbewijzen* is in scope at all, given the live entity is a CV.
- Counsel / DVB: confirm that “we will not deduct” does **not** keep a points-allocated contractual payout out of art. 26 / professional income / possible art. 219.

## Next Steps

- Keep this as an exploration log; do not treat phantom/warrant, nor a labour-minted 10× dividend, as the live spec.
- Next design pass stays **option 2** with reduced complexity unless a later decision picks a contract-token fork **or** a two-instrument residual (cash shares beside the fee).
- Counsel + accountant before anyone is promised phantoms, profit-share tokens, warrants, or a 10× that “is not arm’s length.”
- Do not add an issuer put at a GA-set share price without an effort cap. Do not net warrant exercise against an *inkoop* by Refaqt if the goal is capital-gains / non-fee treatment.
- Do not book a contractual `k × contribution` as a non-deductible dividend in the hope that FPS will skip arm’s length.
