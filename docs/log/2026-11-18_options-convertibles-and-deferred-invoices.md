# 2026-11-18 — Options, convertibles and deferred invoices: a right to equity without a tax event at contribution?

**Role(s):** finance, business-dev

**Path:** cross-cutting. Extends [contract tokens](../../token-system-design/paths/contract-tokens/README.md) (warrants) and [option 2](../../token-system-design/paths/option-2-contingent-fee/README.md) (contingent fee). Adds one sketch that is not yet on the path map: a **convertible contingent fee** (§4).

**Status:** Discussion. Not adopted. No ADR. Design input for counsel and an accountant, not a ruling.

**Prevention rules applied:** [no *inbreng in nijverheid* for unplanned work](../mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md); [share count is not `f(p)` on a share bought at a ticket price](../mistakes/2026-09-04_cheap-share-euro-par.md); [check a second instrument as a pair](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).

## Question

Can call options, put options, convertible or non-convertible shares, a deferred invoice (*uitgestelde factuur*), or an unpaid invoice converted into debt or equity give contributors a right to equity or dividends, **without** a tax event at the moment of contribution?

## The rule underneath every answer

Two facts decide the timing of tax, whatever the instrument is called:

1. **Income tax** is due when income is *certain and determinable* (*zeker en vaststaand*) for a company or a self-employed person, or when a right received for work is **vested, valuable and disposable**. A right that is genuinely contingent and has no market is a hope; it is taxed when it pays.
2. **VAT** on a service is due when the service is completed and the invoice must follow by the 15th of the next month. Only a consideration that is **not determinable** at completion moves VAT to the moment each part becomes payable (C-548/17 *Baumgarten Sports*).

And one company-law fact decides whether **shares** can come out of work: a share is issued against an *inbreng*. Work is *inbreng in nijverheid* (revisor, valued before issuance — dead-end). A receivable is *inbreng in natura* (revisor, valued at conversion). Only cash (*inbreng in geld*) needs no revisor.

So: **deferral needs a contingent, unvalued claim. Equity needs a valued inbreng or cash.** No instrument has both at the same moment. The design question is only *where* the moment of conversion sits and how big the tax is at that moment.

## Instrument by instrument

| Instrument | Tax at contribution? | Equity at the end? | Verdict |
| --- | --- | --- | --- |
| **Deferred invoice** (work now, invoice later, amount fixed) | **Yes.** Income is certain when the work is done; VAT is due at completion. Late invoicing adds fines, not deferral | — | Does not work. Only a **contingent** amount defers, and that is option 2 |
| **Unpaid invoice left as a receivable** | **Yes.** Contributor (BV or self-employed) is taxed on the invoiced amount and pays the VAT before being paid | No | Contributor pre-finances tax and VAT. The company deducts the fee and can recover the VAT |
| **Unpaid invoice → subordinated loan** | Yes, already taxed at invoice. The conversion itself is neutral | No, a loan. Interest: 30% RV for a person; deductible for the company within art. 55 and the 5:1 related-party thin-cap rule (art. 198 §1, 11° WIB 92) | Works, but it is "taxed pay, lent back". Not deferral |
| **Unpaid invoice → shares** (debt-to-equity) | Yes, already taxed at invoice | **Yes, real shares.** Inbreng in natura of a receivable: revisor report at each conversion; batch it yearly. Paid-in fiscal capital = receivable value; later capital repayment can be tax-free (proportional rule). **Not** VVPRbis (needs cash) | Legally clean. Count follows the euro amount of a taxed fee, which is fine: the labour was taxed as labour first. Fails the "no tax at contribution" goal |
| **Contingent fee (option 2)** | **No.** Taxed and VAT due at payout | No | Live path. The only instrument here that actually defers |
| **Contingent fee + right to convert into shares when payable** | No at contribution. **Yes at conversion:** the claim becomes certain, so it is income, and the shares are an inbreng in natura | Yes | New sketch, §4 |
| **Call option / warrant at FMV strike, granted for work** | **Yes, but small.** Optiewet lump sum for a natural person who accepts in writing within 60 days (≈18% of the share value, +1%/year above five years; halved in some cases). For a contributor BV: VAT and VenB on the option's value | Yes, after paying the strike in cash (*inbreng in geld*, no revisor). Later gain on a sale is in principle tax-free for a natural person; dividends on the shares are ordinary dividends | Real, but a BV/NV tool (a CV cannot issue *inschrijvingsrechten*); valuation at every grant; needs cash at exercise; needs a buyer or dividends to pay off. Worth more when the company value is low (§3) |
| **Put option for the contributor** (sell to the company or a founder at a formula) | Usually yes: a put at a known price makes the right valuable at grant. An issuer put at a GA-set price is a disguised fee | Turns equity back into a fee | Avoid, as already ruled in [contract tokens](../../token-system-design/paths/contract-tokens/README.md) |
| **Convertible share class** (e.g. the vote-only governance share converts into a profit class on a work trigger) | Taxed at conversion on the value gained, as professional income | Yes | A conversion triggered by work is pay in kind at that date. No better than §4 and it mixes the governance leg with a profit right ([votes off the reward](../decisions/2026-09-15_votes-off-the-reward.md)) |
| **Non-convertible profit share class issued for work** | Is *inbreng in nijverheid* | — | Dead-end |
| **Certificates via a foundation** (STAK: foundation holds shares, issues certificates with the economic rights) | Received for work → taxed at grant on value; "hard to value" is not "worth zero" | Economic rights only | Same box as profit certificates. No timing gain over the 2026-11-17 scheme |
| **Supplementary pension** (group insurance / IPT for a company director, VAPZ for the self-employed) | **No.** Deductible premium, taxed at payout at a low rate | No equity, but a genuine statutory deferral | Only for employees and company directors (80% rule) or the self-employed (VAPZ cap). Not a contributor-wide tool; noted for completeness |

## 1. "Uitgestelde factuur" does not defer anything by itself

Holding back an invoice does not hold back the tax. The VAT event is completion of the service. The income event is when the amount is certain. Both happen when the work is accepted at a fixed price. The only lever is to make the **amount** genuinely uncertain: payable only from a future pool, which may be zero. That is exactly what option 2's contingent invoice already does. There is no second way.

## 2. Unpaid invoice → debt or equity: clean, but the tax comes first

This route is legally the most ordinary one in the table. It is also the one that most clearly **fails** the stated goal, because the tax and VAT are paid on the day of the invoice, before any cash arrives.

If it is used anyway, two details make it bearable:

- **Pay the VAT part in cash, convert only the net.** The contributor owes the VAT to the state when invoicing; the company recovers the same VAT from the state. Paying 21% in cash and converting the rest avoids the contributor pre-financing a tax the company gets back. Ask the accountant whether the 2023 rules on VAT on unpaid invoices force a correction at the company if the receivable stays unpaid for long.
- **Batch conversions yearly** to keep the revisor cost to one report per year. The receivable is easy to value (nominal, less impairment if the company could not pay it).

The share count then tracks euros of taxed fee, so it tracks work. That is **not** the cheap-share fault: there the dividend label was used to avoid taxing labour as labour. Here labour was taxed as labour first, and the shares are bought with that taxed claim at a revisor-checked value.

## 3. Options when the company is worth little: small tax now instead of no tax

An option at a strike equal to today's fair value has a small taxable value when the company is young and the valuation is low. Under the Optiewet the natural person pays tax once, on a lump sum of that small value, and the later rise in value is not taxed as income. The legislator built this regime **for** rewards caused by work, so a grant sized by contribution is not the labour-quota fault on this instrument.

The limits that kept warrants "open, not pursued" still hold:

- A **CV cannot issue warrants** (*inschrijvingsrechten*). Options would have to be on existing shares (a founder or a foundation as writer) or need a BV/NV vehicle.
- Each grant needs a **valuation**, and grants are discrete, not per ledger row. Yearly grant rounds are the practical shape.
- Exercise needs **cash** from the contributor. Payoff needs a **buyer** or **dividends** on a share class that carries profit rights. QOLAB's planned shares are vote-only; the residual sits on the bond and option 2. An option on a vote-only share at €1 is worth nothing.
- The Optiewet does not apply to a contributor **BV**; that BV pays VAT and VenB on the option's value at grant.
- Confirm current Optiewet rules with the accountant before relying on the rates above.

Verdict: the best fit for "equity for work with a small, early tax", but only if Refaqt runs a share class with real profit rights in a vehicle that can grant options. That is a different product from QOLAB's current CV structure.

## 4. New sketch: convertible contingent fee

Keep option 2 unchanged up to the moment a payout becomes payable. At that moment the contributor may choose, per payout:

- take it in cash (today's option 2), or
- convert all or part of the now-certain claim into shares of a profit-bearing class, at a revisor-checked value, in a yearly batch.

**Timing.** No tax at contribution (the claim is contingent). At conversion the claim is certain, so it is income: VAT and income tax are due on the converted amount, exactly as on a cash payout. The contributor needs cash for that tax, so the natural rule is "pay the VAT and a tax reserve in cash, convert the rest".

**Company side.** The company deducts the fee as in option 2 and gains fiscal paid-in capital instead of paying cash out. That is attractive when the pool exists on paper but cash is tight.

**Risks to check as a pair with option 2:**

- A share class whose holdings come only from converted fees has a count that follows labour euros. That is acceptable (taxed fee, §2), but the administration will ask whether the **issue price** is fair value. A price below value is a benefit in kind at conversion.
- Do not publish a fixed conversion price or ratio. A known euro per share for a known fee per hour rebuilds a unit FX across the two instruments.
- It reopens a profit-bearing share class that the governance leg deliberately avoided. Check against [votes off the reward](../decisions/2026-09-15_votes-off-the-reward.md) and the asset lock.
- CV: each conversion is a capital increase by inbreng in natura (revisor, art. 6:110 WVV). Confirm with counsel.

## Takeaway

- There is **no** instrument that gives a right to equity or dividends for work with no tax until payout, unless the right stays a contingent, unvalued claim. Option 2 is that claim.
- Equity can only be reached at a **conversion moment**, and that moment is taxed. The design choice is how small the tax is there: small and early (options at a low valuation, BV/NV only), or full and late (convertible contingent fee, §4).
- "Deferred invoice" and "unpaid invoice → debt/equity" do not defer tax. They can still be useful to keep cash in the company after the tax is paid.

## Questions for counsel and the accountant

1. Can a CV write a contractual right for a contributor to convert a payable option-2 claim into new shares (inbreng in natura of a receivable, art. 6:110 WVV) without making the option-2 claim itself look like a share right before conversion?
2. Fair-value method for the issue price at conversion in a CV with no market; who signs it besides the revisor.
3. VAT: if the company recovers VAT on a contributor's invoice that stays unpaid and is later converted into capital, does any correction apply?
4. Optiewet: current rates and conditions for options on shares of an unlisted company granted to self-employed contributors; any recent changes.
5. If a BV/NV vehicle were added for an option pool, how it sits beside the CV, the asset lock and the mission lock.
