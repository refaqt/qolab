# 2026-09-10 — Repo review: is the analysis correct, and what does DVB do with a 10× cap?

**Role(s):** finance, business-dev

**Status:** Review of the whole repo against Belgian sources. No ADR. Does not accept, unpark, or revive anything. Design input for counsel, not a ruling. Citation fixes from §3 were applied to [dvb-questions.md](../../token-system-design/dvb-questions.md) in the same pass.

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not keep paid-off `p` as seniority](../mistakes/2026-09-08_unburned-p-after-cap.md); [do not use inbreng in nijverheid to reward unplanned later work](../mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md).

## What happened

Read every document in the repo (design notes, ADRs, mistakes, all logs) and checked the Belgian legal citations and the 2026 rate claims against sources. Then answered the standing question from the [cap-opening log](2026-09-10_pt-distribution-and-cap-opening.md) and DVB **(p)**: will the DVB treat a 10× cap as arm's length, what happens if it does not, does it impose 3×, and does the extra tax land on the contributor.

Headline: **the repo's legal reasoning is largely sound and the 2026 numbers check out**, but three citations are wrong or overstated, one VAT rule is missing that weakens item **(c)**, the general anti-abuse rule is absent entirely, and — most importantly for the goal — **the repo has built the 10× on the one base where it is hardest to defend, and has assumed a ruling can settle `k`, which it almost certainly cannot.**

---

## 1. The 10× question, answered

### 1.1 DVB will very probably never tell you "10× is not arm's length"

That is not how the service works on a question like this.

| Step | What actually happens |
| --- | --- |
| **Prefiling** | Informal, can be anonymous, non-binding. The team says whether it sees a positive decision. Most prefilings never become a formal request; a large share end as *zonder gevolg*, often after negative advice. |
| **Formal request** | You file only if prefiling signalled green. If the team wants a lower `k`, you amend the request before filing. |
| **Positive decision** | Binds FPS **for max five years**, and **only** while the conditions in the decision are met and the facts were completely and correctly described. |
| **Negative decision** | Cannot be appealed. Can be refiled in modified form **if the transaction has not yet been executed**. A negative decision on file is a bad artefact to hold into an audit. |

So there is **no order and no cap**. What exists is a negotiation whose output is a number the team will sign. Functionally that can push you from 10× to something lower — but only if you want the ruling. You can launch at 10× with no ruling at all; you then carry the risk yourself.

### 1.2 There is no "3×" anywhere in Belgian law

`k = 3` is **your own illustrative parameter** from [vintage-pools.md](../../token-system-design/vintage-pools.md) and [ADR 2026-09-03](../decisions/2026-09-03_time-opened-fee-cap.md), not a legal benchmark. The repo already says "no statutory max `k`" in the [cap-opening log](2026-09-10_pt-distribution-and-cap-opening.md) — that is correct and should not drift into a belief that 3× is safe and 10× is not. There is no multiple table. There is only: *would an independent party have agreed this ex ante for this risk?*

### 1.3 The likeliest DVB outcome is that they confirm the box and refuse the number

This is the finding that most changes planning. The repo (README, [token-system.md](../../token-system-design/token-system.md) §"What to take into the next design iteration" item 8, [dvb-questions.md](../../token-system-design/dvb-questions.md) "How to file") assumes a ruling settles `k`. Expect instead:

- **Confirmed:** characterisation (fee, not dividend — item **(b)**), no taxable event at mint (**(a)**), VAT time of supply (**(c)**), contractor vs employee (**(d)**), deductibility timing (**(e)**). These are legal-qualification questions and are squarely rulable.
- **Not confirmed:** whether €50,000 is a reasonable price for €5,000 of documented effort. That is a valuation / appreciation question. The DVB gives decisions on the tax treatment of a described transaction, and the KB of 17 January 2003 already carves tax rates and the calculation of tax out of its remit. Expect a decision that confirms the mechanism **subject to the condition that the remuneration is at arm's length**, which hands the quantum straight back to a future auditor.

**Plan for that.** A ruling that says "this is a fee" and is silent on `k = 10` is a *good* outcome, not a failure — it removes the expensive risks (dividend, wage, tax at mint) and leaves the cheap one (see 1.4). Do not treat "DVB blesses 10×" as a gate before launch, because it is unlikely to exist in that form.

### 1.4 If the multiple is later attacked: **the CV pays, not the contributor**

This is the direct answer to "would contributors just need to pay more taxes?" — **no, not in the base failure mode.**

The repo attaches the quantum test to **art. 49 WIB 92**. That is the wrong hook (see §3.1). The excess-remuneration hook is **art. 53, 10° WIB 92** — costs that *unreasonably exceed professional needs*. Its consequences are materially milder than the repo assumes:

- The **administration carries the burden of proof**.
- Only the **excess portion** may be rejected, not the whole expense. Invoking art. 53, 10° is an admission that the expense is professional.
- Case law forbids the auditor from judging the *opportuneness* of the spend.

Worked failure, one lot: `E = €5,000`, paid **€50,000** (10×), FPS accept 3× and disallow **€35,000**.

| Scenario | CV (Refaqt) | Contributor / their BV |
| --- | --- | --- |
| **Accepted (base case)** | Deducts €50,000 → VenB saved €10,000 (20% band) / €12,500 (25%) | Turnover €50,000, VenB, then extraction at VVPRbis 18% or liquidation reserve ≈18% |
| **Excess disallowed, art. 53, 10°** | Cash **still gone** (€35,000 paid) **and** VenB on the add-back: €7,000 (20%) / €8,750 (25%). Plus nondeductibility of that tax, plus a possible *belastingverhoging* | **Unchanged.** Still declares €50,000, still taxed on it |
| **Requalified as hidden dividend to a member** | No deduction on the **whole** €50,000 (€10,000–12,500) **and** 30% *roerende voorheffing* = €15,000, for which the **CV is the debtor**; if not withheld the base is grossed up. VAT deduction on the "fee" also exposed | Only worse **if** the RV is contractually passed on |
| **Requalified as wage (RSZ)** | Employer contributions + arrears | Employee RSZ + PIT; genuinely worse |

Two consequences the repo should design around:

1. **Size drives deductibility. Shape drives characterisation.** A too-high `k` on an otherwise clean option-2 fee costs the *cooperative* a deduction. It does not by itself turn the payment into a dividend or a wage. Those come from *who* is paid *why* — membership as the key, points as the key, subordination — which the repo already guards well. The repo currently blurs these into one "recharacterisation" fear and therefore over-penalises `k`.
2. **A 10%+ tax increase on the disallowed slice is worse than the headline rate.** Under art. 206/3 §1 WIB 92, losses, DBI, innovation deduction and the other listed deductions **cannot be offset** against a supplement carrying an effective *belastingverhoging* of 10% or more. The Grondwettelijk Hof upheld the mechanism (arresten 19 June 2025 and 9 April 2026) while insisting on proportionality; first-instance courts have set it aside as disproportionate in individual cases. For a CV with carried-forward losses — the normal state of a long-unpaid-contributor cooperative — this converts a "lose the deduction" event into a cash-tax event.

**Nobody has written down who bears that.** Neither the dienstenovereenkomst sketch nor the QOLAB annex says whether a disallowance at the CV is absorbed by the pool (everyone's future `P_t` shrinks) or clawed back from the contributor. That belongs in the annex before anyone is promised anything.

### 1.5 Why 10× is hard here — and it is not the number

**The repo chose the comparable and handed it to the administration.**

The moment the ceiling is written as `k × hours × frozen band`, you have told FPS the market price of the thing: hours × rate. Every euro above 1× then has to be defended as a risk premium *on a stated wage-like benchmark*. That is the worst possible ground for a 10×. [tokens-not-shares §4](2026-09-10_tokens-not-shares-avoid-revisor.md) says this almost exactly ("if lifetime or expected payout ≈ hours × frozen contractor band, that **is** the arm's length quantum") and then the live spec keeps the effort base anyway.

The [Cred/Q log](2026-09-10_cred-value-q-euro-par.md) states the correct principle and then does not promote it:

> Wrong test: "is €15,000 too much for five minutes?" Right test: "would an independent have charged about this **for this outcome**?"

**Three bases, three different fights:**

| Base of the ceiling | What FPS compare against | Can it carry 10×? |
| --- | --- | --- |
| `k × documented effort` (live spec) | Hours × contractor band | Only as an explicit risk premium you must argue every time. Fragile. |
| **Royalty on the products that embody the contribution** | Royalty rates for engineering/design IP (typically low single-digit % of net sales) | **Yes, invisibly.** Nobody divides a royalty by the designer's hours. A 10× lifetime return on effort is an ordinary outcome of an ordinary royalty. |
| Dividend on **cash-subscribed** shares whose count is **not** `f(p)` | Nothing — art. 53, 10° does not test a distribution | Yes, but it is company value, not contribution |

The royalty base is the one path in the repo that reaches 10× **without** an arm's-length argument about multiples, and the repo has it filed as an open fork rather than as the answer to the goal. Its named weakness is real and fixable: an **uncapped** Cred share of *all* Refaqt revenue is residual-claimant-shaped; a royalty **scoped to the products that use the contribution** is a normal commercial contract.

### 1.6 The strongest filing argument for `k = 10` is one the repo has not assembled

Arm's length is tested on the **ex ante** bargain, not the ex post winner. A ceiling that pays 10× only in the branch where a lot waited ~10 years fully unpaid, and 0 in every branch where `P_t` never arrives, has an **expected value near 1×**. That is a standard contingent-fee shape (no cure, no pay), not a 26%/year yield.

The repo has the pieces — `P_t` may be zero, lots expire unpaid, freeze after 1× paid, no opening after repayment — and never puts them together into the one sentence DVB needs. To file it you must also be able to **evidence** it: real years with `P_t = 0`, real lots that lapsed unpaid, and a written policy that does not promise the multiple. Note the tension with [(e)](../../token-system-design/dvb-questions.md) same-year invoicing: the more reliably the pool pays every year, the weaker this argument gets. The [cap-opening log](2026-09-10_pt-distribution-and-cap-opening.md) spots the symptom ("looks like an annual billing cycle") without connecting it to the 10× defence.

### 1.7 Practical recommendation

- Keep option 2 at or near **1×** for ordinary time-based work. Do not spend the arm's-length fight there.
- Put the **10× on a different base**: a scoped royalty / success fee on commercialised outputs (the Cred/Q family), or cash-subscribed shares (structure A). Two bases, two tests, neither carrying the other's weakness.
- If you keep `k = 10` on effort anyway, file it as §1.6 (expected value ≈ 1×, evidenced), accept that DVB will likely not confirm the number, and write the disallowance risk allocation into the annex.

---

## 2. What the repo gets right (checked against sources)

| Claim | Verdict |
| --- | --- |
| "You cannot have both 'not a dividend' and 'not a fee'"; labels lose to facts | **Correct**, and the single most valuable line in the repo |
| Allocation by contribution points is the smoking gun that the cause is labour | **Correct** |
| A CV may issue only registered voting shares and bonds (art. 6:19 WVV) — no *winstbewijzen*, no *inschrijvingsrechten* | **Correct** |
| A CV share may only be issued *in ruil voor een inbreng*; no gratuitous shares | **Correct** |
| *Inbreng in nijverheid* needs a founders'/board report with a motivated valuation **plus** a revisor opinion, **before** the shares exist (arts. 5:7 §1 BV / 6:8 §1 CV) | **Correct**, and the dead-end conclusion follows |
| VVPRbis 18% from 1 July 2026 | **Correct** |
| Dividend exemption €833 / ≈€249.90, income year 2026 | **Correct** |
| 2026 *meerwaardebelasting*: 10%, ~€10,000 annual exemption; *aanmerkelijk belang* threshold 20% (not 10%) | **Correct** |
| DBI: ≥10% or acquisition value ≥€2.5m, 1-year holding, subject-to-tax | **Correct** as stated (confirm the large-company threshold change with the accountant) |
| MiCA: assets technically impossible to transfer to anyone but the issuer are outside scope (loyalty-scheme carve-out, Recital 17) | **Correct** |
| Wait-and-run / idle-pool analysis of `v = pool / N`; capping `N` just moves the price into the GA | **Economically correct** and well argued |
| Proportional burn `p ← p·(rem − alloc)/rem` keeps `p/rem` invariant | **Correct** (algebra verified) |
| Cap-opening arithmetic (1.96× at 12 months, ≈9.4 years to 10×, blend-vs-lots €4,800 gap, the three opening paths) | **Correct** (recomputed) |
| Uniform 100 points/hour only renames hours, and is only dangerous if calibrated to a market wage | **Correct** |
| `(k·E)/Δp` is not a unit FX because the same work at different mint dates gives different `Δp` | **Correct**, though this is the weaker half of the argument — see §4.4 |

---

## 3. What is wrong or overstated

### 3.1 Art. 49 WIB 92 is doing work that belongs to art. 53, 10°

Art. 49 appears ~18 times across the repo as the "not excessive" test. Art. 49 sets the **conditions of deductibility** (incurred in the period to obtain or retain taxable income, and justified). The **excess** test is **art. 53, 10° WIB 92** (*kosten in zover zij op onredelijke wijze de beroepsbehoeften overtreffen*).

This is not pedantry — it changes the risk picture in the design's favour:

- Burden of proof on the administration, not on Refaqt.
- **Partial** rejection only; invoking it concedes the professional character of the expense.
- No review of opportuneness.

Every "art. 49 (not excessive)" in the repo should read "art. 53, 10° (excess), with art. 49 for the conditions of deductibility."

### 3.2 Art. 26 WIB 92 is overstated

[tokens-not-shares §7](2026-09-10_tokens-not-shares-avoid-revisor.md) says art. 26 bites "even if you do **not** deduct." Art. 26 §1 contains an express carve-out: the abnormal or benevolent advantage is **not** added back to the grantor's profit when it is **taken into account in determining the taxable income of the recipient**. Belgian contributors and Belgian contributor BVs that invoice and are taxed on the fee fall inside that carve-out. The exceptions in art. 26 §2 target related foreign / privileged-regime recipients, which is not this fact pattern.

Art. 26 is therefore **not** the main quantum risk here. The conclusion of §7 ("VenB first + 30% WHT + no deduction does not remove arm's length") survives — but it survives on art. 53, 10° and on requalification, not on art. 26.

### 3.3 "DVB + counsel before anyone is promised a certificate" assumes a ruling can settle `k`

See §1.3. The gating assumption in [token-system.md](../../token-system-design/token-system.md) item 8 and in the "How to file" section of [dvb-questions.md](../../token-system-design/dvb-questions.md) should be split: file for the **box**, expect the **number** to come back as a condition rather than a confirmation.

### 3.4 Item (c)'s VAT hypothesis is missing the backstop that will be used against it

DVB **(c)** reasons from art. 22 (taxable event) and art. 26 WBTW (taxable amount) and concludes "VAT on the **invoice** in the year of `P_t` if contingency is real." The missing rule is **art. 22bis WBTW**: for a B2B service, VAT is chargeable when the invoice is issued **and in any case on the fifteenth day of the month following the month in which the art. 22 taxable event occurred**, when no invoice was issued before that date.

So "we invoice later" defers nothing on its own. The defence has to be one of:

- the **service is not yet completed** (a continuous/staged supply), or
- the **consideration is genuinely conditional and undetermined**, so no chargeable amount exists yet — the argument supported by CJEU *baumgarten sports & more* (C-548/17) on conditional successive payments.

Item (c) currently invites counsel to discover the hole rather than pre-empting it. The [cap-opening log](2026-09-10_pt-distribution-and-cap-opening.md) already notes in passing that `Y+1` "does not move VAT" — that instinct is right and needs the art. 22bis citation behind it.

### 3.5 Minor

- The option 1 vs option 2 table in [token-system.md](../../token-system-design/token-system.md) §4 is arithmetically fine, but the "contributor's BV, then VVPRbis 18%" column silently assumes VVPRbis eligibility (shares issued for **cash** from 1 July 2013, small company, fully paid). Many contributor BVs will not qualify. See §4.2.
- "Royalty WHT 30% can also apply to some IP payments" is fine, but the conclusion that engineering/OSS work does not reach the 15% *auteursrechten* regime should note that the post-2023 narrowing was upheld against the IT sector's annulment challenge — it is settled, not arguable.

---

## 4. What is missing

### 4.1 Art. 344 §1 WIB 92 (*fiscaal misbruik*) appears nowhere

The general anti-abuse rule is absent from every document. It is the obvious weapon against the structure the repo is converging on — **structure A, two instruments**: option-2 credits for labour *beside* cash shares carrying the residual 10×. If the cash-share allocation ends up correlating with contribution (and the whole political motive is that it should), FPS can argue the split into two legal boxes is artificial and recharacterise the combined arrangement. This deserves a DVB item of its own and a design rule: the share class must be defensibly **not** `f(p)` — equal per member, or a fixed statutory split — for a reason that exists independently of the tax result.

### 4.2 The liquidation reserve is missing from the extraction analysis

From 1 July 2026 the rate on distributions from a liquidation reserve after the three-year wait rises from 6.5% to 9.8%, which with the ~10% anticipatory levy lands at an effective ≈18% — deliberately aligned with the new VVPRbis 18%. This matters because it gives a contributor BV an ≈18% extraction route **even when VVPRbis does not apply** (older shares, shares not issued for cash, non-small company). The option-2-with-BV column stands, but on a broader footing than the repo currently gives it.

### 4.3 Nothing allocates the disallowance risk

See §1.4. Who eats a €7,000–8,750 add-back: the pool, or the contributor via clawback? Unwritten. This is a contract term, not a tax question, and it should be in the annex.

### 4.4 The `p`-burn makes the (i)/(j) argument harder than the repo admits

[p-burn-remaining-cap.md](../../token-system-design/p-burn-remaining-cap.md) is honest that remaining `p` is now **linear in remaining opened cap** per person, and calls it "more grant-time evidence." That is understated. The strongest leg of the not-a-unit-FX argument is not the algebra (`rem_i/p_i` differs by person) — it is that **a ceiling is not consideration while `P_t` may be zero**. The algebra leg is a second-order point that an auditor can simply decline to be impressed by. Item **(i)** should lead with the ceiling argument and treat the non-uniformity as support, not as the case.

### 4.5 Exit, death and succession are unhandled in the live spec

[ADR 2026-09-02](../decisions/2026-09-02_tax-aware-contribution-credits.md) point 3 allows transfer to treasury, on death, or to a successor vehicle of the same beneficial owner. The live option-2 machinery (`p`, lots, opened cap, freeze, burn) has no rule for what happens to an unpaid opened cap when someone leaves or dies. That is both a contract gap and a tax question (is the lapse a taxable event — the same shape as **(g)**).

### 4.6 The natural-person contributor is not really viable, and that is a cooperative problem

At ~63% combined for a natural person versus ~34% through a BV, the design effectively requires every contributor to run a company. For a model whose premise is broad cooperative contribution, that is a serious adoption constraint and it is not stated anywhere as one. It is not a tax error; it is a product finding that belongs in the architecture note.

### 4.7 Not checked

The CV's *coöperatief doel* (art. 6:1 WVV) against a vehicle whose main activity is rewarding contributor labour; whether *werkende vennoot* case law is quoted at the right strength; whether the DVB has published anything on contribution-token schemes. All three are counsel questions.

---

## Decisions

None as an ADR. Nothing accepted, unparked, revived, or rejected. Applied to [dvb-questions.md](../../token-system-design/dvb-questions.md) in this pass, as citation corrections rather than design changes:

1. Excess test is **art. 53, 10° WIB 92**; art. 49 is the conditions of deductibility.
2. Art. 26 §1 carve-out where the Belgian recipient is taxed on the amount.
3. Art. 22bis WBTW backstop added to **(c)**.
4. New item **(q)**: art. 344 §1 *fiscaal misbruik* on the two-instrument split.
5. **(p)** reframed: ask for the box; expect the number back as a condition; ask what happens to already-opened cap if `k` is later trimmed.

## Open Questions

- Does the goal survive moving the 10× off the effort base onto a **scoped royalty**? If yes, the Cred/Q fork stops being a side sketch and becomes the answer to the stated goal.
- Can the §1.6 expected-value argument be evidenced at launch, before any year with `P_t = 0` has happened?
- Who bears a disallowance — pool or contributor?
- Art. 344 §1 exposure of structure A.
- Counsel: art. 6:1 WVV *coöperatief doel*; exit/death treatment of unpaid opened cap; DVB's appetite for confirming a quantum at all.

## Next Steps

- Decide the base of the 10× before drafting anything: effort with a fragile multiple, scoped royalty, or cash shares.
- Take **(a)–(d)** to prefiling as the box question. Do not make **(p)** the gate.
- Write the disallowance risk allocation into the QOLAB annex.
- Do not publish 10×, `r`, or any ROI language, unchanged from every prior log.

## Sources checked

Belgian ruling procedure and prefiling ([Securex](https://www.securex.be/nl/lex4you/werkgever/themas/verlonen/fiscale-ruling), [VLAIO](https://www.vlaio.be/nl/subsidies-financiering/subsidiedatabank/maatregelen/fiscale-ruling-voorafgaande-beslissing), [DVB annual report 2024](https://www.ruling.be/sites/default/files/content/download/files/jaarverslag_dvb_2024_nl_a4.pdf), [OECCBB commentary](https://blog.oeccbb.be/nl/article/voor-u-gelezen-het-jaarverslag-2024-van-de-dienst-voorafgaande-beslissingen-dvb/28702)); art. 53, 10° WIB 92 ([Practicali](https://www.practicali.be/blog/Onredelijke-kosten-voorwerp-en-bedrag)); art. 26 WIB 92 carve-out ([Lauwers Law](https://lauwers-law.be/abnormale-en-goedgunstige-voordelen/)); art. 206/3 WIB 92 and the tax-increase deduction ban ([Tiberghien](https://tiberghien.com/nl/4638/artikel-206-3-wib92-minimale-belastbare-grondslag-bij-belastingverhoging-van-10-wanneer-de-controlebevoegdheid-van-rechters-hun-creativiteit-de-vrije-loop-laat), [Jubel](https://www.jubel.be/artikel-206-3-wib92-minimale-belastbare-grondslag-bij-belastingverhoging-van-10)); art. 22bis WBTW ([fiscosearch](https://fiscosearch.be/collecties/wetboek-btw/artikel-22bis), [Decostere](https://www.decostere.be/updates/belastbaar-feit-en-opeisbaarheid-van-btw-met-ingang-van-01012016)); VVPRbis and liquidation reserve from 1 July 2026 ([Cazimir](https://www.cazimir.be/en/nieuws/newsflash-nieuwe-programmawet-2026-impact-op-liquidatiereserves-en-vvprbis), [Practicali](https://www.practicali.be/blog/begrotingsakkoord-sleutelt-aan-vvprbis-en-liquidatiereserves)); dividend exemption income year 2026 ([FOD Financiën](https://5398.d8.pr.belgium.be/nl/particulieren/belastingvoordelen/vrijstellingen-dividenden)); *meerwaardebelasting* 2026 ([BDO](https://www.bdo.be/en-gb/insights/news-alerts/2026/capital-gains-tax-on-financial-assets-in-2026-complete-guide), [Baker Tilly](https://bakertilly.be/nl/news/meerwaardebelasting-op-financiele-activa-vanaf-2026-impact-op-beleggers-en-ondernemers/)); *inbreng in nijverheid* reporting ([CBN/CNC advice](https://www.cbn-cnc.be/sites/default/files/2019/draft/NL_Inbreng_in_nijverheid.pdf), [ICCI](https://www.icci.be/nl/rechtspraak/jurisprudence-detail-page/inbreng-in-nijverheid-apport-en-industrie-25-010)); MiCA scope ([Regulation (EU) 2023/1114](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32023R1114)).
