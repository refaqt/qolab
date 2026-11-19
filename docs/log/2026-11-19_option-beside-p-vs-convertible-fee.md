# 2026-11-19 — A share option beside option 2, compared with a convertible contingent fee

**Role(s):** finance, business-dev

**Path:** cross-cutting. Works out the two candidates from [2026-11-18](2026-11-18_options-convertibles-and-deferred-invoices.md): the **convertible contingent fee** (§4 there) and the **call option at today's value** (§3 there). Both sit beside [option 2](../../token-system-design/paths/option-2-contingent-fee/README.md). Neither works with the shares QOLAB plans today (§5).

**Status:** Discussion. Not adopted. No ADR. Design input for counsel and an accountant, not a ruling. Tax rates are rough and must be confirmed by the accountant.

**Prevention rules applied:** [share count never tracks contribution on a share with a profit right](../mistakes/2026-09-04_cheap-share-euro-par.md) — §2 says where an option is different and where it is not; [a second instrument must not publish the comparable](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md) — the option's tax form is a compelled document (§2.4); [no *inbreng in nijverheid*](../mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md); [no euro price per hour](../mistakes/2026-09-03_unit-price-on-growing-pool.md).

## Questions

1. With option 2 (`p` weights, a share of the yearly pool, a ceiling that opens over time), the contributor also gets the right to **buy shares at today's value**. How does that differ from the convertible contingent fee?
2. Can the convertible contingent fee convert at the share price **of the moment of contribution**?
3. What changes if work is counted in **milestones and deliverables** instead of hours?
4. What does "needs checking against the governance design and the asset lock" mean?

## Short answers

1. They are two different deals. The **option** is a second right, granted for the work, taxed a little at grant, and it gives the contributor the **growth in share value** from grant to exercise. The **convertible fee** is one right: the fee itself, which the contributor may take as shares instead of cash at the price of the day it is paid. It is taxed in full at that moment and gives **no** growth before conversion.
2. Yes, legally. But the difference between the old price and the price on the day of conversion is then **pay for the work**, taxed as income on the day of conversion, without cash to pay it. The clean way to get the old price is the option plus the fee **as two separate instruments**: the fee pays cash, and the contributor uses that cash to exercise the option (§3).
3. Milestones help. They remove "hours × rate" as the comparable and fit discrete option grants. They do **not** change when tax is due: that still depends on the amount being uncertain. They bring new problems: how to define and accept a milestone, and how to pay work that is not a milestone (§4).
4. Today QOLAB's planned shares are worth exactly €1 forever and carry no profit. An option or a conversion into those shares is worthless. To make either worth something, Refaqt needs a share class with real profit rights. That class would vote, would reopen the asset lock, and needs the veto holder's approval (§5).

## 1. The two instruments side by side

### 1.1 What each one is

**Option beside `p`.** When a piece of work is accepted, the contributor receives two things:

- `p` weight, as today. It pays a share of the yearly pool, up to the opened ceiling, as an invoiced fee.
- A **call option**: the right to buy a number of shares at a fixed price (the *strike*) equal to the fair value of a share **on the grant date**, during a fixed term (for example 5 to 10 years).

**Convertible contingent fee.** The contributor receives only `p`, as today. When a payout becomes payable, they may choose cash, or new shares at the fair value **on the payout date**, paid for by turning the claim into capital.

### 1.2 Worked example

A share is worth €10 when the work is accepted. Three years later it is worth €40. The option-2 payout in that year is €5,000 (plus VAT).

| | Option beside `p` (500 options at €10) | Convertible fee, price of the payout day | Convertible fee, price of the contribution day |
| --- | --- | --- | --- |
| At contribution | Tax on the option's lump-sum value: about 18% × €5,000 = **€900 taxable** (natural person, Optiewet). No VAT for a natural person outside VAT; a contributor BV pays VAT and corporate tax on the option's value | Nothing | Nothing |
| Year 3: fee | €5,000 invoiced and taxed as income | €5,000 taxed as income | — |
| Year 3: shares | Pays €5,000 cash (can be the fee, after tax) → 500 shares worth **€20,000** | €5,000 claim → 125 shares worth **€5,000** | €5,000 claim → 500 shares worth **€20,000** |
| Taxed income in year 3 | €5,000 (the fee). The €15,000 growth is **not** income at exercise under the Optiewet | €5,000 | **€20,000**: the fee plus the €15,000 discount, all as pay for work |
| Later sale of the shares | Gain in principle tax-free for a natural person (normal management of private assets) | Same | Same, from €20,000 |
| Company deducts | The €5,000 fee. Not the €15,000 growth (that is dilution, not a cost) | €5,000 | €5,000; the €15,000 discount is very likely not deductible |
| Company law | Exercise for cash = *inbreng in geld*, no revisor | Conversion of a claim = *inbreng in natura*, revisor report | Same, plus a report on why the price is below value and what it costs the other shareholders |

The option gives the same €20,000 of shares as conversion at the old price, but the growth is taxed as a small lump sum **at grant** instead of as income **at conversion**. That is the whole point of the option, and it is the reason the legislator made the Optiewet.

### 1.3 The differences in one table

| | Option beside `p` | Convertible contingent fee |
| --- | --- | --- |
| Number of rights | Two: fee and option | One: the fee, with a choice of how to take it |
| Tax at contribution | Yes, small, on the option | None |
| Tax at payout | The fee, as income | The fee, as income, whether cash or shares |
| Who gets value growth before payout | The contributor | Nobody extra; shares at the price of the day |
| Cash needed by the contributor | The strike, at exercise | The tax on the converted amount |
| Company deduction | The fee only | The fee only |
| Works in a CV | Only as a contract to subscribe new shares later, or an option on existing shares written by someone who holds them. A CV cannot issue warrants (*inschrijvingsrechten*) | Yes, as a capital increase by contribution of a claim |
| Valuation needed | At **every grant** (the strike) | At **every conversion** (the issue price) |
| Risk for the contributor | If shares do not rise, the option is worth nothing, and the tax at grant is lost | None beyond option 2 |

## 2. The option in more detail

### 2.1 Optiewet basics (confirm with the accountant)

- Applies to a **natural person** who gets an option because of their professional activity: employee, director, or self-employed contributor.
- The person must **accept in writing within 60 days** of the offer. Then the taxable benefit is a fixed lump sum at grant: **18% of the share value** for a term up to 5 years, plus 1% for each extra year. Under extra conditions (for example no exercise before the end of the third calendar year after the offer) the lump sum is halved.
- After that, exercise and sale are **not** taxed as income. Dividends on the shares are ordinary dividends (30% withholding tax).
- If the person does **not** accept within 60 days, the full gain is taxed as income at exercise. That is the worst outcome.
- A contributor **BV** cannot use the Optiewet. The BV pays VAT and corporate tax on the option's value at grant, and later holds shares like any company shareholder.
- An option on an unlisted company needs a value per share at each grant, set by an expert or by a method an expert confirms.

### 2.2 Why this is not the cheap-share dead-end, and where it still is

The cheap-share fault was: shares at a ticket price, count set by hours, and the payment called a dividend so that labour is **never** taxed as labour.

The option is different in three facts:

- The grant **is** taxed as labour income, under a regime the legislator built for rewards caused by work.
- The strike is **fair value**, paid in **cash**. The contributor buys at the same price an outsider would pay that day.
- Dividends later are paid on shares bought at fair value, so they follow capital.

It is still the same fault in one fact: **the number of options follows the work**. The repo's binding rule says "share count never tracks contribution on a share with a profit right." This option breaks the letter of that rule. Adopting it would need an ADR that writes an exception: "allowed only when the grant is taxed as income at grant and the strike is fair value paid in cash."

### 2.3 Paying the strike with the option-2 payout

The contributor can use the option-2 fee, after tax, to exercise. That is allowed and common, as long as:

- the fee is paid out and the contributor freely decides to pay in; no contract obliges them to reinvest it;
- the two payments are separate: the CV pays the invoice, the contributor pays the strike into the capital account;
- nobody nets them into one booking. Netting is a conversion of a claim (*inbreng in natura*, revisor) or a buyback, not a cash exercise.

### 2.4 Pair check against option 2

Option 2's defence depends on there being **no euro price per hour of work**. The option can publish one by accident:

- The Optiewet benefit appears on a **tax form** the company must issue (a compelled document). If grants are "N options per hour", that form states euros of benefit per hour.
- So grants must **not** be per hour. Grant per milestone (§4) or in a yearly round decided by the board, with no published rate.
- The strike (fair value per share) must never appear in the same document as a contributor's ceiling or `p`.

## 3. Conversion at the price of the contribution day

Three ways to write it, from worst to best:

1. **Fixed conversion price inside the fee claim.** The claim converts at the old price. Result: the discount is pay for work on the conversion day, taxed as income without cash to pay it (row 3 of the example). It also needs a revisor and a special report on the low price. Not recommended.
2. **Conversion right treated as an option.** A right granted at contribution to convert a future claim at a fixed price may qualify as an option under the Optiewet, but paying the strike by setting off a claim is not normal practice. Ask counsel and the accountant. Even if it qualifies, it still needs the revisor because the shares are paid with a claim.
3. **Option plus fee as two instruments (recommended).** §2.3. The fee is taxed as a fee. The option fixes the old price and is taxed at grant. The cash exercise needs no revisor.

So the answer is yes, but only route 3 is clean. Routes 1 and 2 bring the tax to the conversion day.

## 4. Milestones and deliverables instead of hours

### 4.1 What improves

- **The comparable changes.** A fixed amount per hour lets the administration compare with a wage. A quote per deliverable is how outside contractors are normally paid. The option-2 spec already allows a quoted effort in the annex instead of hours × band.
- **Option grants fit milestones.** Each accepted milestone is a grant date with one valuation. That is a discrete grant, which is what the Optiewet expects, and it avoids "N options per hour".
- **The mint can use weights fixed before the work.** For example, each milestone gets a size (small, medium, large) agreed when it is planned. `p` is minted from that size, not from euros.
- **A quality gate can come with it.** The 2026-09-12 log already sketched a machine check of the deliverable (for machine work: the project checks pass).

### 4.2 What does not change

- **Tax timing.** A milestone with a fixed price is a finished service with a known price: income and VAT are due at acceptance. Only a contingent amount (a share of a pool that may be zero) moves tax to payout. Milestones change the measure, not the timing.
- **The labour link.** Options or `p` per milestone still follow work. The ADR exception in §2.2 is still needed.
- **A milestone price is still a price.** If each milestone has a euro quote, that quote is the comparable, now per deliverable instead of per hour. It is a weaker comparable, but it is one. Keep the euro quote as a **ceiling** only, as option 2 does with hours × band.

### 4.3 New problems

- **Definition and acceptance.** Someone must write each milestone before the work and accept it after. Disputes about scope replace disputes about hours.
- **Work that is not a milestone.** Maintenance, administration, support, and reviews do not end in a deliverable. They need a fallback: a role milestone per quarter, or hours for those roles only.
- **Unfinished work earns nothing.** A contributor who does 80% of a milestone and leaves gets nothing unless partial acceptance is defined.
- **Gaming.** Milestones can be cut small to get more grants at a low valuation. The board, not the contributor, should set the size.

## 5. Governance design and asset lock: what the check means

### 5.1 What QOLAB plans today

From the [governance leg](../../token-system-design/paths/governance-voting/README.md) and [ADR 2026-09-15](../decisions/2026-09-15_votes-off-the-reward.md):

- The CV has **one class of vote-only shares** at €1. A member may hold a number that follows the square root of their recent contribution. They pay **no dividend** and are always returned at **€1**.
- Investors hold a **bond** and have **no vote**.
- An **asset lock** in the statutes says the company's net assets can never flow to members beyond what they paid in. On liquidation, the surplus goes to an organisation with a similar mission.
- A **veto share** (class G), held by a foundation, must approve any change to the asset lock and the mission.

### 5.2 Why that matters for an option or a conversion

1. **There is nothing to gain.** A share that is always worth €1 has a "today's value" of €1 and a value in ten years of €1. An option on it is worthless. A conversion of a fee into it turns a fee into a €1 deposit.
2. **A profit class breaks the asset lock.** To make the option worth something, the share must take part in profit or in the liquidation surplus. That is exactly what the asset lock forbids. Changing it needs the veto holder and a special majority, and the mission constraint says to reject a design whose only story is private profit.
3. **Shares in a CV always vote.** A CV can only issue registered voting shares. Shares from options or conversions would bring votes that follow work or fees. That puts votes on the reward, which ADR 2026-09-15 rules out, unless the new class has a vote ceiling (the cash-shares path suggests at most 5% of the votes present and no vote on reserved matters).
4. **A CV cannot issue warrants.** The option must be a contract to subscribe new shares later, or an option written by someone who already holds shares.

### 5.3 Ways out, if the option route is wanted

| Way out | What it means | Cost |
| --- | --- | --- |
| **A capped profit class in the CV** | Shares with dividends up to a cap, and a fixed share of the liquidation surplus; the rest stays locked for the mission | Needs the veto holder, a statute change, and a vote ceiling. The cap limits the option's upside |
| **A separate product company (BV or NV)** | The CV keeps its lock and governance. A BV or NV that runs a commercial product line can issue real warrants to contributors | Two companies, transfer pricing between them, and a mission lock in the BV too |
| **Keep the upside off shares** | Use the [scoped royalty](../../token-system-design/paths/scoped-royalty-cred-q/README.md) or a capped bond instead | No equity, which was the point of the question |

## 6. Follow-up questions

The example used throughout: Ann gets an option on 500 shares at €10 (a share is worth €10 at grant), and three years later the shares are worth €40.

### 6.1 Who sets the €10, and is that a revisor every time?

- The Optiewet wants the **real value of the share on the date of the offer**. For an unlisted company that is a valuation, not a market price. If the company has a statutory auditor (*commissaris*), the auditor normally confirms it. A small CV usually has none; then an external accountant or a *bedrijfsrevisor* can do the valuation, using one method that stays the same every year.
- This is **not** the revisor report for a contribution in kind. That report is needed only when shares are paid with something other than cash. A cash exercise needs no such report.
- If the strike is set **below** the value, the difference is added to the taxable amount at grant.
- Practical shape: **one valuation per year** and **one grant date per year** (or two) for all milestones accepted since the last round. Not one valuation per milestone.
- Counsel and the accountant confirm who may sign the valuation for a CV without a statutory auditor.

### 6.2 What if there is no payout within the option term?

- The option does **not** depend on payouts. Ann may exercise with her own savings.
- If she does not, the option expires. She loses the tax already paid at grant; it is not refunded.
- Five years without any profit usually also means the share is not worth much more than €10. So in that case the option was worth little, and the loss is mainly the tax at grant.
- The term can be **longer**: up to 10 years. Each year above five adds 1% to the taxable lump sum (10 years: 23% instead of 18%).
- Do **not** plan to extend the term later. A change to the terms can count as a new grant and be taxed again.
- Refaqt should **not** lend Ann the money to exercise. Company law limits a company that finances the purchase of its own shares (financial assistance), and a cheap loan is a taxable benefit.

### 6.3 Is it about 9% tax today on unpaid work?

No. The **work itself is not taxed** today: the `p` weight is a contingent claim. Only the **option** is taxed.

- 18% is **not** a tax rate. It is the part of the **share value under option** that counts as income: 18% × 500 × €10 = €900 of income.
- That €900 is then taxed at Ann's own rate (roughly 25–50%), plus social contributions for a self-employed person (about 20.5%). On €5,000 of shares under option that is roughly **€450–€650**, so about **9–13% of the share value under option**, not of the value of the work.
- The **halved** lump sum (9%) applies under extra conditions, for example: no exercise before the end of the third calendar year after the offer, and the option cannot be sold or given to someone else. Then it is roughly 4.5–6.5% of the share value under option.
- The tax grows with the **number of options** and the **share value at grant**. Both are choices. Grants made while the company is still worth little cost almost nothing.

### 6.4 Where did €13,500 come from, and what was the work worth?

The number was chosen so that, after tax, about €5,000 was left to exercise. In option-2 terms it can be read like this (illustration only; no document may state a euro amount per hour):

- Documented effort when the work was accepted: **€9,000** (the hours times the frozen band, or a quote per milestone). That is what Ann would have invoiced if she had been paid at once, plus VAT.
- The ceiling then opens while the work stays unpaid. With the illustrative `r = 0.25`, the ceiling is 1.25× after one unpaid year and 1.50× after two: **€13,500**.
- The payout is Ann's share of the pool, limited by that ceiling. In this example the pool was large enough to fill it.
- Under ADR 2026-09-14 (two bases, proposed) the multiple for time-based work stays near 1×. A smaller `r` or `k` gives a payout closer to €9,000.

### 6.5 Contributors who work through their own company (BV)

The Optiewet is only for natural persons. A contributor BV that receives the option is paid **in kind** for its services.

| Step | Ann as a natural person | Ann's BV |
| --- | --- | --- |
| Option at grant (value about €900) | €900 counts as income: about €450–€650 tax and social contributions | VAT 21% (€189, paid by the CV in cash and recovered by the CV) and corporate tax about 20% (€180) |
| Fee of €13,500 | About 63% tax and social contributions: about €5,000 left | Corporate tax 20%: €10,800 stays in the BV. Taken out through the liquidation reserve or VVPRbis at about 18%: about €8,860 for Ann |
| Exercise (€5,000 for shares worth €20,000) | No tax | No tax. The BV pays from its own cash |
| €15,000 growth when the shares are sold | In principle not taxed | Corporate tax about 20% (a small holding gets no exemption), then about 18% out: about €9,840 for Ann |
| Dividends on the shares | 30% withholding tax | 30% withheld (creditable), corporate tax in the BV again, then 18–30% out |

So the BV is better for the **fee** (about 34% instead of about 63%) and worse for the **share growth** (about 34% instead of 0%). The best mix would be: the BV invoices the fee, and Ann **personally** receives the option under the Optiewet. Ask the accountant whether that holds when the work is done through her BV; the halved 9% lump sum is often refused to the manager of a management company.

## Takeaway

- If equity is wanted, the **option beside option 2** is the better of the two: a small tax at grant, value growth taxed as capital, a cash exercise without a revisor, and the fee can fund the exercise.
- The **convertible contingent fee** is simpler and works in the CV as it is, but it gives no growth and is taxed in full at conversion. Converting at the old price only moves the tax to the conversion day.
- **Milestones** are a better measure than hours for both, mainly because they fit discrete option grants and weaken the wage comparable. They do not defer tax.
- **Neither instrument is worth anything with today's €1 vote-only shares.** The real decision comes first: does QOLAB want a share class with profit rights at all, inside the asset-locked CV or in a separate company?

## Questions for counsel and the accountant

1. Current Optiewet conditions and rates for options on shares of an unlisted CV or BV granted to self-employed natural persons; whether a contractual right to subscribe new CV shares counts as an option.
2. Whether a right to convert a future option-2 claim at a fixed price can be taxed as an option at grant.
3. Whether a capped profit class can sit inside the asset lock without making the lock leonine or unclear.
4. Valuation method for a CV share at each grant when there is no market and the asset lock limits what a share can receive.
5. If a separate BV or NV is used for an option pool: how to keep the mission lock there, and how its profit relates to the CV's pool `P_t`.
