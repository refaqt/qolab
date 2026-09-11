# 2026-09-11 — Cheap-share route again: linear A quota, €100 B class, 10-year sunset

**Role(s):** finance, business-dev

**Status:** Same rejection as the [cheap-share dead-end](../../token-system-design/cheap-share-route.md) for all four combinations. Not a new option, not an ADR. Confirms [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md). Design input for counsel, not a ruling. The **sunset** is the one genuinely new object; §5 and §8 say where it is worth keeping.

**Prevention rules applied:** [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not put a euro spot price on certificates](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not use inbreng in nijverheid to reward unplanned later work](../mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md). Token-engineering: labels do not take compensation outside VAT or income tax; facts beat labels.

## What happened

Re-ran the cheap-share route with four modifications and asked for legal/tax analysis of two cases, each with and without a 10-year sunset.

- **Case 1.** `p_i = c_i / 1000`. `p_i` sets how many **class A** shares a contributor may buy. A is **€1 in issue price and in liquidation value**. Contributors buy `p_i` A shares. Profit `P_t` (after VenB) is distributed as a dividend by **ratio of shares owned**.
- **Case 2.** Adds **class B** at **€100** price and liquidation value. Dividends go by **number of shares**, not by value paid in. B is open to anyone, mainly investors.
- **Sunset variant.** After 10 years a share stops receiving dividends (no dividends on shares more than 10 years old).

New relative to earlier passes: the mint is **linear and published** (1,000 points → 1 share), price **equals** liquidation value, the class gap is **100:1 at €1/€100** rather than €0.10/€10, and there is a **time limit on the profit right**. Everything else (quota = `f(work)`, dividend per share, no cap, no burn) is the [2026-09-08 variant](2026-09-08_option-1-tenth-vs-ten-euro-shares.md) and the [2026-09-10 no-investors variant](2026-09-10_no-investors-euro-shares.md).

---

## 0. Direct answers

| Question | Working answer |
| --- | --- |
| Can Belgian company law write any of the four? | **Yes, and more cheaply than the earlier sketches.** Classes with divergent profit rights are allowed (arts. 6:40, 6:46 WVV; disproportionate profit sharing is permitted as long as it is not a full profit monopoly). A €1 issue price is fine in a capital-less CV. Exit at paid-in value is already the CV **default** for the *scheidingsaandeel*. The plumbing is not the problem. |
| Does any of the four win option 1 (30% dividend, no VAT, no tax at grant)? | **No.** In all four the **number of shares is `f(hours)`**. That is the fact the whole file has rejected five times. Linear mint, par-equals-liquidation-value, an investor class and a sunset all leave it untouched. |
| Does `p = c/1000` help because it is simple and carries no bonding curve? | **Neutral at best.** It removes the curve objection and adds a **published, linear labour→share rate** (at 100 points/hour: **1 A share per 10 hours**). Simpler to explain, easier for an auditor to read off. |
| Does "price = liquidation value" remove the benefit in kind? | **No.** It removes the discount on the *capital* content only. The value of an A share is the PV of its dividend stream, not its €1 *scheidingsaandeel*. Subscribing at €1 to a share worth more than €1 is a benefit; the €1 par is not the reference price. |
| Does the €100 B class make A look like capital by comparison? | **It does the opposite.** B is the comparable FPS did not previously have: at these parameters the statutes say **1 contributor hour ≡ €10 of investor capital** (§4.1). That is a euro rate on work, published in the statutes. |
| Does the 10-year sunset help? | **It fixes economics and worsens characterisation.** It bounds dilution of B to a steady state (§4.2) and answers "a perpetual claim is equity-like." But a profit right that expires 10 years after the work is the signature of **deferred pay for that work**, it is easier to value at grant (so **more** grant-time tax risk), and it splits class A into one **soort per vintage** (§5). |
| Which of the four is least bad? | None is usable as a dividend. Case 1 without sunset is quietest on **pricing** evidence (no second class, no published euro comparable) and loudest on **allocation** (100% of residual profit follows hours). Case 2 with sunset is loudest on both. |

---

## 1. What each modification changes

| Modification | Company law | Tax characterisation | Economics |
| --- | --- | --- | --- |
| `p = c/1000`, linear | Neutral | **Worse.** A published rate of shares per point; with 100 points/hour it reads as 1 share / 10 hours | Removes early-bird; simplest ledger in the file (only `c`) |
| A price = A liquidation value = €1 | Fine; matches the CV default *scheidingsaandeel* (paid-in, capped at NAV if lower) | Small help: no discount on the capital content. Does **not** price the dividend right | Fixes the [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md) "A drains the CV at NAV on exit" problem |
| No cap, no burn | Fine | Neutral to worse: no bound at all on what labour takes | Unbounded dilution of B without a sunset |
| B at €100, dividend **per share** | Writable (statutory disproportionate profit split) | **Worse.** Publishes the labour/capital FX; makes the €99 per share transfer visible on the face of the statutes | B is un-investable unless A issuance is capped or matched |
| 10-year sunset | One **soort per vintage**, or *uittreding van rechtswege* (§5) | **Worse at grant** (bounded stream is valuable and valuable-to-value), better against "perpetual = equity-like" | Bounds A's steady-state share; pressures the GA to distribute before shares expire |

None of these is the load-bearing fact. **`N_A = f(c)` is**, and it is in all four.

---

## 2. The quota, once more (short)

A CV share may only be issued **in ruil voor een inbreng** (art. 6:39 WVV). €1 in cash is formally *inbreng in geld*. If **how many** shares you may subscribe is set by hours, the real contribution is work → *inbreng in nijverheid* (art. 1:8 WVV), which must be valued before issuance, with a report and normally a **bedrijfsrevisor** — the trigger the whole file is avoiding, and a [dead-end](../decisions/2026-09-10_inbreng-in-nijverheid-dead-end.md) as a reward path in any case. Paying €1 does not turn labour into a cash contribution.

Two operational consequences that are easy to get wrong:

1. **The €1s must be real money in.** Netting the subscription against anything the CV owes the contributor is *inbreng van een schuldvordering* → revisor and valuation of past labour ([tokens-not-shares §7](2026-09-10_tokens-not-shares-avoid-revisor.md)).
2. **A quota you may exercise later is an option.** If unused `p` can be converted into A shares in a future year at €1 when the company is worth more, that is an option on cheap shares, with its own grant-time regime (Optiewet, 60-day acceptance, valuation of an unlisted company — [tokens-not-shares §6](2026-09-10_tokens-not-shares-avoid-revisor.md)). Either require subscription in the period the points are logged, or give the quota a short expiry, or accept option taxation.

---

## 3. Case 1 — A only

### 3.1 Without sunset

Internally this is the **most proportionate** structure in the file: every share costs €1, every share gets the same dividend, so dividend per share = dividend per euro of *inbreng*. There is no value transfer between shareholders at all. The entire labour reward sits in **who was allowed to subscribe**.

That is also why it fails. With no other class, **100% of residual profit follows hours, forever**. This is verbatim the [2026-09-10 no-investors variant](2026-09-10_no-investors-euro-shares.md): louder deferred pay, not a cleaner dividend. *Werkende vennoot* case law wants profit as a return on **capital at risk** in a joint enterprise; capital at risk here is €1 per 10 hours.

No cap and no burn means no bound on lifetime extraction — the objection [vintage-pools.md](../../token-system-design/vintage-pools.md) raised against an unlimited lifetime share of every future `P_t`.

### 3.2 With sunset

Now the tail stops. Three consequences:

- **Where does the residual go?** A shares have a €1 *scheidingsaandeel* and, after year 10, no profit right. If contributions ever stop, no share is entitled to profit and no share has NAV upside. The accumulated surplus then belongs to **nobody unless the statutes name a taker** (reserves, a purpose, another class). That must be written. As a design this is steward-ownership shaped — which is a legitimate thing to build, but it is the **opposite** of the capital-at-risk story option 1 needs.
- **Characterisation gets worse, not better.** A profit right that expires exactly 10 years after the work that generated it is a **10-year payment plan for that work**. Equity does not evaporate on an anniversary.
- **Grant-time valuation gets easier.** A bounded stream can be valued; a perpetual contingent one is harder. The uncertainty that helps deferral ([token-system.md](../../token-system-design/token-system.md) §1) is the uncertainty of the *pool*, and the sunset does not touch that — but it removes the "unbounded and unquantifiable" half of the argument.

---

## 4. Case 2 — A at €1, B at €100, dividend per share

### 4.1 The statutes publish a euro price for an hour

Dividend per share with a 100:1 price gap is a **chosen conversion rate between labour and capital**, as [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md) already named it at €0.10/€10. What is new is that with `p = c/1000` it is now **computable and published**:

```
€ of B capital per contributor hour = B price × points per hour / points per A share
                                    = 100 × 100 / 1000 = €10 / hour
```

So the statutes say: one hour of work buys the same dividend claim as €10 of investor money. FPS do not have to build a comparable — the company wrote one. This is the prevention rule [do not put a euro spot price on contribution credits](../mistakes/2026-09-03_unit-price-on-growing-pool.md), re-entering through the issue-price ratio rather than through `w` or `v`.

It is also the number to sanity-check as a *design* matter: at 100 points/hour, the design values a contributor hour at €10 of subscribed capital. Change the points scale or the B price and that rate moves; it is not a neutral choice.

### 4.2 Dilution of B, with and without the sunset

Assume 1,800 contributor hours/year (→ 180 A shares/year, €180 of cash in) and one investor holding 300 B shares (€30,000).

| Year | A stock | A share of dividends | B share of dividends |
| ---: | ---: | ---: | ---: |
| 1 | 180 | 37.5% | 62.5% |
| 3 | 540 | 64.3% | 35.7% |
| 5 | 900 | 75.0% | 25.0% |
| 10 | 1,800 | 85.7% | 14.3% |
| 15 | 2,700 | 90.0% | 10.0% |
| → ∞ | → ∞ | → 100% | → 0% |

**With the 10-year sunset**, A's earning stock is a rolling 10 vintages, so it converges instead of diverging: 1,800 A shares, **A 85.7% / B 14.3%, permanently**. Steady state is `10·a_A / (10·a_A + N_B)`.

That is the sunset's real structural job: **it converts unbounded dilution into a fixed steady state.** It does not make B whole. For a 50/50 steady state at these parameters B must hold 1,800 shares = **€180,000** against 18,000 contributor hours — i.e. **€10 of investor capital per contributor hour**, the same FX as §4.1, which is the design's built-in exchange rate however you scale it.

### 4.3 The rest of Case 2

- **Investor protection.** Uncapped A issuance decided by a GA in which A holders vote is a value transfer from B to A on a continuing basis (*vennootschapsbelang*, abuse of majority, directors' duties). A real investor prices this in or refuses. If A issuance is capped to make B investable, the cap is a labour budget — option 2 with extra steps.
- **Voting.** A CV may issue only registered **voting** shares and bonds (art. 6:19 WVV). If one A share is one vote, contributors control the CV long before they hold most of the capital. The classic cooperative answer — **one member, one vote** — decouples governance from the quota and is consistent with the file's rule that the **governance share is not the reward**.
- **B is an offer to the public.** "Can be bought by anyone" is the first variant in this file that leaves member-only territory. Below €5,000,000 over 12 months there is no prospectus, but a public offer generally requires an **informatienota** published via FSMA (KB 23 September 2018); recognised cooperatives have their own exemptions. Note what the information note would have to disclose: that contributors acquire identical dividend rights for €1, that A issuance is uncapped, and the dilution path in §4.2. Marketing B without that is a misrepresentation problem, not just a regulatory one.
- **VVPRbis for B.** The reduced rate requires that **no preferential right** as to participation in capital, in profit, or in the distribution of the company's assets is attached to *the shares claiming the benefit* (art. 269 §2 WIB 92); other shares carrying preferences do not by themselves disqualify. Two questions for counsel: whether A's identical per-share dividend at 1/100 the price is a *voorkeurrecht* in the technical sense (probably not — it is a different issue price, not a preference), and, **in the sunset variant, whether B's non-expiring profit right is itself a preferential right that costs B the reduced rate**. That last point is a real risk in the combination the user asked about.

---

## 5. The sunset as a legal object

The user's sunset is "no dividends on shares more than 10 years old." Two ways to write it, with different costs.

| Route | Mechanics | Cost |
| --- | --- | --- |
| **Per-vintage classes** | A share whose rights differ from another share is, by definition, a different **soort** (art. 7:60 WVV for the NV; Book 6 analogue for the CV, with art. 6:87 governing creation/amendment of classes). A dividend right keyed to issue date means **A-2027, A-2028, …** are separate classes by operation of law, whether or not the statutes say so | 10+ live classes at all times; class-by-class voting and reports on any amendment (art. 6:87); register must track vintage |
| **Automatic withdrawal** | Buy the share back / let it lapse at €1 on its 10th anniversary. A CV can tie membership to a statutory *hoedanigheid* whose loss triggers **uittreding van rechtswege** (arts. 6:121–6:122 WVV); on withdrawal the shares are destroyed, and the *scheidingsaandeel* defaults to paid-in value capped at NAV — exactly €1 here | One class, much simpler. But forced redemption at par after a decade of dividends is the "the share was never equity" fact from [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md). Distribution tests apply to the payment |

Two more points:

- **Leonine question at the tail.** A clause denying a shareholder (or class) any participation in profit is void (art. 4:2 WVV; the BV rule of art. 5:41 says each share participates in the profit **or** the liquidation balance, with statutes free to set the proportion). A post-sunset A share keeps a €1 liquidation entitlement, so it probably still "participates." Counsel item — do not assume it, and do not write a share that has neither.
- **Governance side effect.** Holders with ageing vintages want the GA to **distribute before their shares expire**. That is the mirror image of the old burn design's "retain until the fat year" ([mistake 2026-09-04](../mistakes/2026-09-04_cheap-share-euro-par.md)) and is genuinely healthier, but it is pressure to pay out cash the CV may need, against WVV net-asset and liquidity tests.
- **Anti-abuse.** A sunset has a defensible **non-fiscal** rationale (keep the reward with active contributors, rotate ownership), which is useful against art. 344 §1 *fiscaal misbruik* — [DVB item (q)](../../token-system-design/dvb-questions.md). It does not repair the allocation key.

**Net:** the sunset bounds **duration**, not **amount**. Ten years of dividends on an uncapped share is still unbounded in euros, so it does not answer the arm's-length quantum question at all.

---

## 6. What the prize is, and what the failure costs

Per €10,000 of CV margin before VenB, paid to one natural person (indicative, income year 2026; SME band 20%).

| Route | CV keeps a deduction? | Levies | Net to contributor |
| --- | --- | --- | --- |
| These cases, dividend box **holds**, RV 30% | No | VenB €2,000 + RV €2,400 | **€5,600** (~44%) |
| These cases, dividend box holds **and** VVPRbis 18% | No | VenB €2,000 + RV €1,440 | **€6,560** (~34%) |
| Option 2, natural person invoices | Yes | Social + PIT | ~€3,700 (~63%) |
| Option 2 through the contributor's BV, extraction ≈18% | Yes | BV VenB €2,000 + ≈18% | ~€6,560 (~34%) |
| Recharacterised as professional income | No (already not deducted) | VenB **already paid**, then PIT + social ≈63% of the €8,000, VAT 21% on top, RV credit messy, possible *belastingverhoging* / art. 219 | ≈**€3,000**, with VAT and interest still to settle |

Two honest observations.

1. **The prize is real and it is the answer to [§4.6 of the repo review](2026-09-10_arms-length-10x-and-repo-review.md)** ("the natural-person contributor is not viable"). If the dividend box held *and* VVPRbis applied, these cases would put a natural person at ~34% without needing a BV. That is the first structure in the file that does so. It is why the idea keeps coming back.
2. **The quota is what stops it.** Both conditions are exactly what `N_A = f(hours)` destroys: the box, because allocation by contribution is the smoking gun that the cause is labour; and VVPRbis, because it is a dividend regime and does not survive a requalification into professional income. The failure mode is not "we pay 44% instead of 34%" — it is the last row, with VenB already sunk.

---

## 7. What does **not** change from previous passes

- No deduction for the CV: the reward is paid out of post-VenB profit, so the same euros as an option-2 fee would have reduced VenB first ([token-system.md](../../token-system-design/token-system.md) §4).
- Employment / RSZ: unchanged. Private-person shareholders and "no employees" help only if there is no subordination; a share quota per hour worked is close to a piece rate.
- MiCA / DAC8: irrelevant here — these are registered shares in a register, not tokens.
- You still pick **one** box. A dividend on shares *and* "this is the reward for contributions" on the same instrument is how you get 30% **and** VAT/PIT/RSZ.

---

## 8. What is worth keeping out of this pass

1. **The sunset, moved to the fee side.** A time limit on a contribution weight is already half-specified in this repo: lapse of a lot after `T` periods is **DVB item (g)**, and the live option-2 path already has lots, an opened cap and a freeze. "Weights stop being eligible for `P_t` 10 years after the work" is the same idea with none of the class/vintage machinery and no dividend story. If the sunset is the part the user likes, that is where it belongs.
2. **An active-member class that is not `f(hours)`.** The open option-1 sketch from [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md) gets a mechanism from this pass: **one equal share per contributing member**, with membership tied to a statutory *hoedanigheid* ("active contributor"), whose loss triggers *uittreding van rechtswege* (arts. 6:121–6:122 WVV) and destruction of the share. Count tracks **whether** you participate, not **how much** you worked, which is what a CV's *coöperatief doel* is for. It gives labour a statutory share of profit and a rotation rule without a quota. It does **not** give "more hours → more dividend"; that leg stays option 2.
3. **Price = liquidation value.** Keeping the *scheidingsaandeel* at paid-in value (the CV default) is right in any variant and kills the "labour class drains the CV at NAV" failure from 2026-09-08.
4. **The €10/hour FX as a calibration check.** Whatever instrument is used, computing the implied euro-per-hour before shipping is a cheap test that the parameters mean what was intended.

If the political goal is "contributors who work more get more of the upside," that **is** the labour quota, and it is an option-2 question — as [tokens-not-shares §7](2026-09-10_tokens-not-shares-avoid-revisor.md) concluded. You cannot have the quota, skip the revisor, skip arm's length, and keep a clean 30% (or 18%) dividend.

## Decisions

Proposed (not a new ADR):

1. **Reject all four combinations** as an option-1 path. Linear `p = c/1000`, par equal to liquidation value, a €100 investor class with per-share dividends, and a 10-year sunset do not cure `N_A = f(work)`. Confirms [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md).
2. **Do not publish a labour↔capital issue-price ratio.** Two classes with equal per-share dividends and a 100:1 price gap state a euro price for an hour. Treat that as the same class of fact as `w`, `v = pool/N` and 1 `p` = €1.
3. **Keep the sunset as an option-2 object** (lapse of weights / lots, DVB **(g)**), not as a share right.
4. Note the variant on [cheap-share-route.md](../../token-system-design/cheap-share-route.md) and extend the prevention rule in [docs/mistakes/2026-09-04](../mistakes/2026-09-04_cheap-share-euro-par.md) to the sunset and the €1/€100 pair.

## Open Questions

- Counsel: whether a vintage-keyed dividend right creates a *soort* per vintage in a CV (Book 6 analogue of art. 7:60), and what art. 6:87 then requires on every amendment.
- Counsel: whether *uittreding van rechtswege* on loss of an "active contributor" *hoedanigheid* (arts. 6:121–6:122) is a clean way to run both the sunset and the active-member class, and how the distribution tests apply to paying the €1 *scheidingsaandeel*.
- Counsel: leonine-clause exposure of a post-sunset share with no profit right and a €1 liquidation entitlement (art. 4:2 WVV; BV analogue art. 5:41).
- Counsel / accountant: in Case 2 with a sunset, does B's non-expiring profit right count as a *voorkeurrecht* under art. 269 §2 WIB 92 and cost B holders VVPRbis?
- FSMA: informatienota scope if B is offered to anyone, and what must be disclosed about uncapped A issuance.
- Where the residual goes in Case 1 with a sunset, once no share carries a profit right and every share exits at €1.
- Whether the active-member class in §8.2 deserves its own option-1 sketch — still the open question from [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md) and [2026-09-10](2026-09-10_tokens-not-shares-avoid-revisor.md).

## Next Steps

- Do not promise contributors A shares, a per-hour share quota, or 30%/18% treatment on any of these four.
- If the sunset is wanted, specify it on **weights** in the next option-2 pass and file DVB **(g)** with it.
- If an option-1 residual is wanted beside option 2, sketch the **active-member equal-share class** (not `f(p)`), with the art. 344 §1 point from [DVB (q)](../../token-system-design/dvb-questions.md) in mind.
- Counsel + accountant on the items above before any statutes are drafted.

## Sources checked

VVPRbis "no preferential right" condition, art. 269 §2 WIB 92 ([Monard Law](https://monardlaw.be/nl/stories/ingelicht/vvprbis-regime-bijkomende-verstrengingen/), [Practicali](https://www.practicali.be/blog/verstrenging-van-het-vvpr-bis-regime)); classes defined by the rights attached and amendment of class rights ([Corporate Finance Lab](https://corporatefinancelab.org/2023/01/17/kapitaalverhoging-en-soorten-van-aandelen/), [Monard Law](https://monardlaw.be/nl/stories/ingelicht/wvv-vraagstuk-2-hoe-moet-een-controleverslag-bij-wijziging-van-de-rechten-verbonden-aan-soorten-praktisch-worden-benaderd/)); leonine clause and disproportionate profit sharing under the WVV ([Odigo](https://www.odigo.eu/nl/nieuws/journal/het-toepassingsgebied-van-het-verbod-op-leonijnse-bedingen-na-het-wvv-mogelijkheid-tot-disproportionele-winstverdeling), [elfri.be](https://www.elfri.be/artikel/leeuwenbeding)); *scheidingsaandeel* on withdrawal and *uittreding van rechtswege* ([CBN/CNC advice](https://www.cbn-cnc.be/nl/adviezen/uittreding-en-uitsluiting-lastens-het-vennootschapsvermogen-bij-de-bv-en-cv), [Corporate Finance Lab](https://corporatefinancelab.org/2025/01/22/het-scheidingsaandeel-bij-de-statutaire-uittreding-en-uitsluiting-in-bv-en-cv-een-van-de-grootste-anomalieen-in-het-vennootschapsrecht/)); prospectus exemption and informatienota for public offers ([FSMA](https://www.fsma.be/nl/faq/1-welke-gevallen-moet-er-een-prospectus-worden-gepubliceerd-en-welke-gevallen-een), [Cera](https://www.cera.coop/nl/cooperaties/nieuws/2018/20181004-wijziging-prospectus-wet)). Rates and prior verdicts reused from the [2026-09-10 repo review](2026-09-10_arms-length-10x-and-repo-review.md).
