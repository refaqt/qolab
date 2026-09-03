# QOLAB profit-certificate iteration (Belgian law)

Working analysis of the 2026-09-03 bonding-curve design (`2026-09-03_token-system-calculation.ods`) under Belgian VAT, income tax, company law, and EU financial regulation. This is **design input for counsel and an accountant**, not a ruling and not a substitute for a Dienst Voorafgaande Beslissingen (DVB) ruling.

Previous sketch (C / R / U tokens, contractor invoice at cash-out): [docs/log/2026-09-02_belgian-token-system-analysis.md](../docs/log/2026-09-02_belgian-token-system-analysis.md) and proposed [ADR 2026-09-02](../docs/decisions/2026-09-02_tax-aware-contribution-credits.md). This note supersedes that mechanics description; the legal hooks (WBTW arts. 22, 22bis, 26; substance over form) still apply.

**Prevention rules applied:** none yet in `docs/mistakes/` (folder empty). Token-engineering rule that applies here: labels (“profit certificate”, “voluntary contribution”, “cooperative spirit”) do not take compensation outside VAT or income tax. Facts beat labels.

---

## Direct answers

| Question                                                                                                                                                                   | Working answer                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Does the withdrawal rate put a **price** on the certificates, so VAT/tax is due at grant even if profit is unknown?                                                        | **It is evidence of a euro value, and that is the risk.** A published €/certificate rate is the same class of fact as yesterday’s U = €1 peg. Uncertainty of the *pool* helps (a hope is not yet income). A running mark-to-market in euros hurts. Tax is not automatic at grant if the right is non-transferable, the pool is GA-discretionary, and cash may be zero — but the rate is what FPS would use if they argue there *was* consideration.                                                           |
| How else to decide how many certificates to burn per euro?                                                                                                                 | Do **not** derive burn from a bonding-curve euro rate. At payout, set value from **actual money**: `v = pool / certificates outstanding` (or split the pool only among those who opt in, and leave the rest). Burn `euros_received / v`. Early-bird stays in the **mint** `p = c0 · c^k`, not in a rising euro price.                                                                                                                                                                                         |
| Are cash-outs **dividend tax** (30%)? How to avoid? Rename? Revenue claim?                                                                                                 | If the instrument is a member’s claim on **after-tax profit**, decided by the GA, with WVV distribution tests: **yes, 30% roerende voorheffing** (plus the €833/year exemption on the PIT return). Renaming does not help. A **fixed % of revenue** is usually **not** a dividend (it is a cost / royalty) — that *avoids* 30% WHT but *creates* VAT + professional income, and if the % is unconditional it is easier to tax at grant. You cannot have both “not a dividend” and “not a fee”.                |
| Members buy a small share; work is “voluntary”; certificates are a profit claim. Is grant still a paid service (VAT + tax)? Cooperative spirit? Normal CV, not recognised? | **Very likely still paid work.** Membership does not immunise. Unpaid volunteer status (Wet 3 juli 2005) is a poor fit for a profit-distributing CV. Allocation by **contribution points** is the smoking gun that the cause is labour, not shareholding. A normal CV (not NRC / not social enterprise) may distribute profit more freely (no 6% cap), which helps option 1 economically and **hurts** the volunteer story.                                                                                   |
| Option 1 (member + dividend 30%) vs option 2 (contractor + invoiced royalty/fee): lowest tax burden?                                                                       | **On paper, option 1 is cheaper for a natural person** (~30% WHT vs ~55–65% PIT+social, VAT 21% cash-flow). **It is the weaker characterisation** when certificates track work. If it is recharacterised, you can get professional tax **and** lost deduction **and** penalties. For a contributor who invoices through a BV, option 2 with VVPRbis extraction can match or beat a 30% dividend **and** the CV deducts the fee. VVPRbis almost certainly **does not** apply to non-share profit certificates. |

**Can you implement it like this?** The economics (early-bird mint, non-transferable rights, GA pool, burn on cash-out) can be implemented. The legal wrapper “volunteer member, unpriced profit right, tax only 30% at cash-out” is the part that likely does **not** survive Belgian tax and social-security facts.

---

## How this iteration works (from the spreadsheet)

Bonding curve: `p = c0 · c^k` with `k ≈ 0.737`, `c0 ≈ 26.293` (calibrated so that at 250k contribution points, 250k certificates have been minted, and the next 250k points mint 40% fewer incremental certificates).

- `c` = cumulative contribution **points** (effort/value).
- `p` = cumulative **profit certificates**.
- A contribution of `Δc` mints `Δp = p(c_new) − p(c_old)`. Later `Δc` mints fewer certificates.
- Withdrawal rate `w = dc/dp = 1 / (c0 · k · c^{k−1})`, in **euro per certificate**. In the example it rises from about **€0.38** to **€0.70** as `c` goes from 2,000 to 20,000.
- At a withdrawal date: pool is known; holders offer certificates; cash paid = `min(Σ offered · w, pool)`; each holder’s cash is their share of that total; certificates burned = `cash / w`; leftover pool stays.

Worked example (Alex / Bill / Christina, 2027–2029): the first €5,000 pool is almost fully taken by Bill because he offered nearly all of his certificates; later rounds leave leftover when few certificates are offered **because `w` caps extraction**. That cap is the distinct job of the euro rate. Early-bird already exists in the mint (`Δp / Δc` falls).

Because `k < 1`, `w → ∞` as `c → ∞`. A holder who never withdraws can see the euro ceiling per remaining certificate rise without bound if the cooperative keeps attracting contribution. Burning certificates caps **how fast** you extract at today’s `w`; it does **not** cap lifetime euros if you wait. Unlimited *annual* drain is avoided only together with a finite pool (GA). Unlimited *lifetime* pay is not avoided — and you stated that waiting may pay more. That is capital appreciation of the certificate.

---

## 1. Withdrawal rate, price, VAT and tax at grant

### What Belgian tax looks at

- **VAT (WBTW):** a service is taxable when performed (art. 22); the taxable amount is everything received or to be received, **including non-cash**, at value (art. 26; VAT Directive art. 73). There must be a direct link between the supply and the consideration (Tolsma, C-16/93). Genuinely contingent success fees can wait until the fee crystallises; a right that already has an ascertainable euro value can be consideration **now**.
- **Income tax:** Belgian practice on tokens, warrants and benefits looks at **vesting + ability to dispose**, not at the later conversion into cash. A mere hope (no pool, no claim, no market) can stay untaxed. A vested right with a published euro price is the opposite fact pattern.
- **Voucher analogy:** a single-purpose voucher whose VAT amount is known at issue is taxed at issue. A multi-purpose / uncertain voucher waits. A certificate with a public `w` in €/unit looks more like the first than like a spaarpunt without monetary value.

### Does uncertainty of profit save you?

**Partly, not reliably.** Two different uncertainties get mixed:

| Uncertain thing                                         | Tax effect                                                                                                                        |
| ------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Whether the GA will put money in the pool, and how much | Supports “no income yet” — no receivable, no dividend, no fee                                                                     |
| How many euros **one certificate** is “worth”           | The withdrawal rate **answers that question** even when the pool is €0. It is a notional ceiling, but it is a number FPS can copy |

Non-transferability still matters: without a market or a put, disposal is weak, which helps deferral. The spreadsheet nevertheless computes `w` **on every contribution row**, so at grant each holder can say “my new certificates are currently worth `Δp · w` euros if the pool is large enough.” That is a mark-to-market.

### Recommendation on burn without a grant-time price

Keep the bonding curve as a **mint function only**. Do not store or communicate a euro rate at contribution time.

At each distribution date, pick one of:

1. **Pool / outstanding (preferred).** `v = pool / P_outstanding`. Opt-in holders receive `offered · v`. Unoffered certificates leave their share in the pool. Burn `cash / v` (= offered, if they take the full `v`). `v` exists only when there is real money, so it is a payout-time conversion, not a grant-time price.
2. **Split only among those who offer, no curve rate.** `cash_i = pool · offered_i / Σ offered`. Burn all offered (or a GA-set fraction). Leftover is zero unless you separately cap the round (e.g. max 10% of profit). This needs an explicit round cap if you want leftover pool when few people offer — that was the job of `w`.
3. **Dimensionless exhaustion.** Each round, at most a fraction `f` of each holder’s balance may be offered (policy). Cash is pro-rata of the pool among offered. No euros per certificate in the rules.

Do **not** use `w = dc/dp` as a published FX rate. If you need the “few offerers cannot vacuum the pool” behaviour, use (1) or a GA cap, not a bonding-curve euro price.

The “wait and `w` rises” feature is a second early-bird stacked on the mint. It is also the feature that makes the certificate look like an appreciating investment. Drop it; early-bird in `Δp` is enough.

---

## 2. Dividend tax at cash-out — and the revenue-pool fork

### If it is a dividend

Standard facts for a **dividend** (art. 18 WIB 92; roerende voorheffing usually **30%**):

- Paid to a **shareholder** (or holder of a profit right attached to membership).
- Out of **after-tax profit** (VenB 20% SME band / 25%).
- After WVV **net-asset / liquidity** tests and a **GA (or delegated) distribution decision**.
- Not deductible for the CV.

Then:

- Withholding **30%** at payment / attribution.
- First **€833** of dividends per person per year (income year 2026) can be recovered on the PIT return (~€249.90). Negligible for this system.
- **VVPRbis** (18% from 1 July 2026 on qualifying distributions, after the waiting period) applies to **shares issued for cash contributions** in a small company, not to a work-minted “profit certificate”. Do not plan on 18%.
- No VAT on a genuine distribution.
- No social contributions if the dividend characterisation **holds**.

Calling it something else does not help. Calling it a dividend **does** help only if the facts match the list above.

### If it is a revenue share

A **fixed percentage of gross revenue** (your 10% fallback):

- Economically a **royalty / revenue-share cost**, not a dividend.
- Deductible for the CV if it is a professional expense (art. 49 WIB 92) and arm’s length enough.
- VAT and professional income (or royalty WHT) follow the **fee** analysis, not 30% dividend.
- If the 10% is **automatic**, holders have an unconditional claim on turnover. That is the grant-time tax / debt / FSMA pattern you wanted to avoid. GA discretion is what keeps it contingent.
- Paying 10% of revenue can exceed profit and insolvent the CV. Keep a `min(policy %, cash, solvency)` cap.

**You cannot use a revenue pool to keep dividend treatment.** Dividend law needs profit after tax and a distribution decision. If the administration would reclass a profit-certificate payout as a dividend and you therefore switch to revenue, you have **accepted option 2** (cost + VAT), not “dividend with a different name”.

### Avoiding 30% at cash-out

Only by **not being in the dividend box**:

- Contingent **success fee / royalty** invoiced by a contractor (option 2), or
- No cash (pure reputation), or
- Capital reduction / share buyback (different, usually worse, not for this).

There is no clean “profit right for work, taxed at 30%, no VAT, no tax at grant” box in Belgian law when the allocation key is labour.

---

## 3. Small share + voluntary member work + profit certificates

This is the cooperative-spirit hypothesis. It is understandable; it is not how Belgian tax, VAT or volunteer law typically read the facts.

### Membership

Contributors **may** be members. For a CV they often **should** be, if they vote on surplus. That is governance, not a tax exemption.

A normal CV (not recognised by the Nationale Raad voor de Coöperatie, not “erkend als sociale onderneming”) can distribute profit under its statutes without the **~6% of paid-in capital** cap that hits recognised social enterprises (art. 8:5 WVV — “any patrimonial advantage whatsoever” to shareholders). That is useful if option 1 were real. It also means you are a **profit-distributing company**, not a volunteer organisation.

### Volunteer law

The Wet 3 juli 2005 (vrijwilligers) is built for organisations that are not a vehicle for profit distribution to the workers. The Hoge Raad voor Vrijwilligers has been **unfavourable** to volunteer use in cooperatives generally, and only discussed it for recognised CVSO / CV-as-SO **without** profit transfer to members. A normal CV that later pays those same people via profit certificates is not “unpaid member work”. It is **deferred pay**.

Buying a share for a small amount does not convert labour into a hobby. Cassation and labour courts look at **subordination** (Arbeidsrelatiewet) and at whether the “profit share” is in substance **wage**. Labels lose.

### VAT

No consideration → no taxable supply. Profit certificates allocated **because of contribution points** **are** consideration (non-cash). Membership does not create a VAT exemption for labour supplied to a CV that sells on the market.

If the administration accepts that there is **no supply** (pure member participation, no link between this person’s work and this person’s certificates), VAT stays off. That only works if certificates are **not** minted from that person’s points. Equal per member, or per share, might be a member surplus. Points-for-certificates is a supply.

### Income tax at grant of the certificates

Receiving a **share for cash** is not income (you paid). Receiving a **profit right for work** is the same family as a bonus, warrant or token-for-work:

- If the right has no value and cannot be disposed of: argument to defer until cash (your goal).
- If the right is a priced certificate: argument to tax at grant (the failure mode).
- If the right is a real class of shares from **inbreng in nijverheid** (art. 1:8 WVV: a commitment to supply labour as a contribution, in return for shares): the **shares** must be valued. That is often **worse** than a contingent fee — tax on the value of the shares when issued, then 30% on later dividends. Inbreng in nijverheid also brings non-compete and incapacity rules (shares can lapse). It is a company-law tool, not a tax shelter.

**Werkende vennoot** case law: a member who invested money and works to make *that capital* yield can take a profit share without it automatically being wage — if there is real **affectio societatis**, no subordination, and the profit is a return on the joint enterprise, not a disguised salary. Your design pays for **points**, including to people whose cash inbreng is trivial. That is the opposite of “return on a €100 share”.

### Company law of the instrument

A CV’s native instruments are **shares**, possibly in **classes** (soorten aandelen) with different profit rights, written in the statutes. Classic **winstbewijzen** are an NV-style security. A free-floating “profit certificate” that is not a share class is likely just a **contractual claim**. Contractual claims for work are fees, not dividends.

If you want option 1 at all, put the right **in the statutes as a share class**, issued only to members, non-transferable, with GA distributions. That still does not stop tax recharacterisation when the number of class-B shares equals contribution points.

### Employment / social

If the CV organises the person’s time, tools, and hierarchy, RSZ can claim **employment** even if they hold one share. Then salary must be in euro (loonbeschermingswet), tokens are a benefit in kind, and the cost is PIT + employee/employer social. That is the worst case. Keep contractors genuinely independent, or employees on payroll — not a third “volunteer member” labour force.

---

## 4. Option 1 vs option 2 — tax burden

Indicative **income year 2026** figures for a Belgian resident. Not a computation. SME VenB **20%** on the first band; otherwise **25%**. PIT top rate **50%** + municipal ~**7%** of PIT. Self-employed social ~**20.5%** (deductible for PIT). VAT **21%**. Dividend WHT **30%**.

Compare **€10,000 of CV earnings before the reward and before VenB**, paid to one person.

|                                  | Option 1 — dividend (if it holds)    | Option 2 — natural person invoices a fee/royalty                | Option 2 — contributor’s BV invoices, then VVPRbis 18% |
| -------------------------------- | ------------------------------------ | --------------------------------------------------------------- | ------------------------------------------------------ |
| Deductible for the CV?           | No                                   | Yes                                                             | Yes                                                    |
| VAT                              | No                                   | 21% on the fee (CV recovers if fully taxable; else a real cost) | Same                                                   |
| CV VenB on this €10,000          | €2,000                               | €0                                                              | €0                                                     |
| Contributor levy                 | 30% WHT on €8,000 = €2,400           | Social ~€2,050 + PIT/municipal ~€4,250                          | VenB €2,000 in their BV + WHT €1,440                   |
| **Cash in contributor’s pocket** | **~€5,600** (+ up to €250 exemption) | **~€3,700**                                                     | **~€6,560**                                            |
| Combined tax on the €10,000      | ~44%                                 | ~63%                                                            | ~34%                                                   |
| Social rights                    | None                                 | Yes (self-employed)                                             | Depends how they extract                               |
| Legal robustness here            | **Weak** if minted from points       | **Strong** if documented services + invoice at cash-out         | Same, plus extra company                               |

**If the €10,000 is already an after-tax “profit pool”:** option 1 withholds €3,000 and the member nets **€7,000**. That is the attractive pocket math. It ignores that the CV already paid VenB to create that pool, and that the same €10,000 as a **deductible** fee would have reduced VenB.

**Royalty label (option 2):** Belgian “auteursrechten” at 15% is a special regime for original copyright (reformed and capped). Open-hardware / engineering labour generally **does not** qualify. An invoiced “royalty” for work is taxed as a **professional service** (VAT 21% + PIT + social), not as 15% copyright. Royalty WHT 30% can also apply to some IP payments; it is not a saving vs a normal invoice.

**Lowest burden that is likely to stick**

- Natural person, no company: option 1 **looks** cheaper but is the recharacterisation magnet. Option 2 is expensive but honest.
- Person with a BV: option 2 is often **cheaper than a 30% dividend** and the CV deducts.
- Do not pick option 1 “because 30% < 60%” without a DVB ruling. If FPS treat the cash-out as professional income, you may have **no deduction** (booked as dividend), **PIT + social**, possible **VAT**, and **tax increases**.

**Recharacterisation / employment failure mode:** treat as wage → RSZ employer + employee + PIT. Combined can exceed option 2 by a wide margin. This is the reason not to run a volunteer labour pool inside a CV.

---

## Regulatory screen (short)

| Topic             | This iteration                                                                                                                    | Safer variant                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| MiCA              | Off-chain + non-transferable: outside MiCA if there is no technical possibility to transfer to anyone but the issuer (Recital 17) | Keep issuer-only; no peer transfer (you already dropped sales — good) |
| E-money           | `w` in €/certificate is a **par-like** unit, even if the pool formula does not always pay `w`                                     | No euro unit until cash exists                                        |
| FSMA / prospectus | Members-only statutory rights are usually not a public offer; a contractual revenue share sold as an investment would be          | No ROI language; no offer to non-members                              |
| DAC8              | Avoid public crypto rails                                                                                                         | Off-chain ledger                                                      |

---

## What to take into the next design iteration

1. **Pick the tax box first, then fit the curve.** Option 1 = statutes + share class + GA dividend + allocation that looks like capital, not points. Option 2 = services contract + contingent invoice + points as **weights**. Mixing them is how you get both 30% *and* VAT.
2. **Keep members for governance** (small cash share, one member one vote or as statutes say). Do not pretend the share is the reward.
3. **Mint with `p = c0 · c^k`.** Do not quote `dc/dp` in euros.
4. **Burn using payout-time `v = pool / outstanding` (or a GA round cap).** Leftover pool without a published price.
5. **Pool = GA policy** with solvency: `min(p% of profit or EBITDA, optional q% of revenue, cash)`. Not an automatic 10% of turnover.
6. **Non-transferable**, off-chain, no peer market (already in this iteration — keep it).
7. **Employees stay on euro payroll.** QOLAB is not wages in kind.
8. **DVB + counsel** before anyone is promised a certificate. Ask explicitly: (a) no taxable event at mint; (b) characterisation of cash-out as fee vs dividend; (c) VAT time of supply; (d) RSZ / arbeidsrelatie.

Until those sign-offs exist, treat this document as a **pre-legal spec**, not a launched scheme.
