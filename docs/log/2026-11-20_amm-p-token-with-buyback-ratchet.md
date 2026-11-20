# 2026-11-20 — Transferable `p` token on an x·y = k curve with a 10% buyback and a "never falls" price

**Role(s):** finance, business-dev

**Path:** new sketch, on the path map as **Transferable AMM `p`-token with buyback ratchet**. Closest live paths: [option 2](../../token-system-design/paths/option-2-contingent-fee/README.md) (contingent fee) and the [capped participating bond](../../token-system-design/paths/capped-participating-bond/README.md).

**Status:** Discussion. Not adopted. No ADR. Design input for counsel and an accountant, not a ruling.

**Prevention rules applied:** [steep curve vs low grant value](../mistakes/2026-09-07_steep-curve-low-grant.md); [immediate multiple → gold rush](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [unit price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [euro par on a reward unit](../mistakes/2026-09-04_cheap-share-euro-par.md); [check a second instrument as a pair](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).

## The proposal

Replace invoices and shares with tokens:

1. Contributors earn contribution tokens `c`, converted to `p` tokens on a bonding curve.
2. `p` gets a euro price from a Uniswap-style `x · y = k` pool (`p` against euros).
3. At the start the price is very low. Refaqt puts **10% of revenue** into buying `p` from the pool, which raises the price.
4. Contributors may sell `p` at any time, for example to pay the tax on receiving it ("20% company tax → sell 20%").
5. Refaqt adds mechanisms so the price **can only rise**, even after a large sell-off.

Unlike every earlier path, this one **accepts tax at contribution**. Earlier paths were designed to avoid that. This changes the premise, and it reopens the "no unit FX" constraint, which existed mainly to keep tax at payout. If the change is wanted, it needs its own ADR. This note does not decide it.

## 1. Mechanics: points 2, 4 and 5 cannot all be true

On an `x · y = k` pool **every sale lowers the price**. That is the formula, not a side effect. "Anyone may sell at any time" and "the price never falls" can only hold together if someone buys every sale at the current price. That someone is Refaqt, and the commitment has no limit.

Worked example (pool seeded with €1,000 and 1,000,000 `p`, so `k = 10⁹`, price €0.001):

| Step | Pool € | Pool `p` | Price | Note |
| --- | --- | --- | --- | --- |
| Start | 1,000 | 1,000,000 | €0.001 | Contributors receive 500,000 `p` outside the pool during the year |
| Refaqt buys with €20,000 (10% of €200k revenue) | 21,000 | 47,619 | **€0.441** | ×441. Contributors' 500,000 `p` "worth" €220,500 at spot; pool holds €21,000 |
| One contributor sells 50,000 `p` (10% of contributor holdings) | 10,244 | 97,619 | €0.105 | Receives €10,756. Price −76% |
| …or sells 100,000 `p` (20%, "to pay the tax") | 6,774 | 147,619 | €0.046 | Receives €14,226. Price −90% |

Consequences:

- **The spot price is not a value.** Market cap (price × supply) is many times the euros in the pool. Whoever sells first is paid. Later sellers find an empty pool. This is a bank-run shape.
- **"Sell 20% to cover the tax" breaks the price** for everyone else as soon as more than one person does it. If the price is propped up instead, the tax was assessed on a value nobody can realise.
- **Early-mover capture.** Grants at €0.001 followed by a buyback-driven ×441 repeat the [2026-09-07 dead-end](../decisions/2026-09-07_bonding-curve-shares-dead-end.md) and the [gold-rush mistake](../mistakes/2026-09-03_immediate-multiple-gold-rush.md). The first contributors get most of the value. Later contributors get tokens at a high price with little room left to rise.
- **"Never falls" can be built only in three ways**, and each one changes the instrument:
  - (a) **No sells.** Then there is no liquidity for tax, which defeats point 4.
  - (b) **Refaqt buys all sells at the floor.** That is a redemption obligation, a debt of Refaqt equal to floor price × outstanding supply. It sits on the balance sheet and grows with every ratchet step. It also makes the token look like a capital-guaranteed investment product.
  - (c) **Sells queue and are filled only from the 10% buyback budget**, at a price that only ratchets up. This is honest and workable, but it is no longer an AMM. It is a redemption window (§4).

## 2. Tax (Belgium)

- **At grant:** `p` received for work is professional income at **fair value** at receipt.
  - **Contributor BV:** VenB at 20% (on the first €100k, if the conditions are met) or 25%. Getting cash out to the person is taxed again, so about 34% combined (see [analysis §4](../../token-system-design/analysis/belgian-tax-and-company-law.md)). "Sell 20%" therefore covers only the first layer.
  - **Natural person:** progressive income tax plus social contributions, about 63% combined at the margin. Selling 20% does not cover it.
- **Fair value is not the spot price of a thin pool that Refaqt controls.** The FPS can argue that a token backed by a standing 10%-of-revenue buyback is worth about the present value of that stream divided by supply, whatever the pool shows on day one. A near-zero grant value followed by a ratchet funded by Refaqt is exactly the pattern of "pay low at grant, take the remuneration as a capital gain". Expect a requalification under art. 344 §1 WIB 92 or the professional-income rules.
- **On the gain:** for a natural person, the new 10% capital gains tax on financial assets including crypto (Law of 6 April 2026, gains from 1 Jan 2026, €10k yearly exemption) is the *best* case. A gain on tokens obtained through one's own work for Refaqt is at risk of being treated as professional income or as *diverse inkomsten* (33%). For a BV the gain is simply taxed at VenB.
- **VAT:** work paid in tokens is a barter. A VAT-registered contributor owes VAT on the fair value of the service. In practice Refaqt pays that VAT in cash and recovers it, so this costs cash flow but not money.
- **Refaqt side:**
  - The grant is deductible at fair value (art. 49 WIB 92, excess test art. 53, 10°).
  - The **buyback** is the open question. If `p` is not a legal claim on Refaqt, buying and burning it is a payment with no clear deductible basis, and the FPS may read it as extra remuneration.
  - If `p` *is* a claim on Refaqt, the buyback repays a liability and the outstanding tokens are on the balance sheet (§1b).
- **Compared with option 2:** the token model taxes **twice in timing**: once at grant on a value nobody can realise, and again on the gain. Option 2 taxes once, at payout, in cash. For contributors the token model is **worse** on tax, not better. What it adds is liquidity and a simpler story.

## 3. Regulation

The first question is **what `p` is**. MiCA covers only crypto-assets that are *not* financial instruments.

- **Transferable security?** `p` is transferable and negotiable, and its value comes from the issuer's revenue (buyback and burn ≈ revenue share). Under ESMA's guidelines on qualifying crypto-assets as financial instruments it is likely a **transferable security**. Then MiCA does not apply. The **Prospectus Regulation** and Belgian law (law of 11 July 2018: *informatienota* between €500k and €8M, prospectus above) apply instead. Running the pool where anyone can buy is a continuous public offer and arguably a trading venue (MTF), which requires a licence.
- **If not a security → MiCA Title II ("other crypto-assets").** An offer to the public needs a **white paper** notified to the FSMA, with marketing rules and liability.
  - Art. 4(2) exemptions: fewer than 150 persons per member state, a small total offer over 12 months, or qualified investors only.
  - Art. 4(3)(a) "offered for free" does **not** apply. Tokens given for work are not free, because Refaqt receives a benefit.
  - The exemptions fall away if admission to trading on an EU crypto-asset service provider (CASP) platform is sought (art. 4(4)).
- **Operating the pool** means exchanging crypto-assets for funds with proprietary capital as a business. That is a **CASP service** (art. 59 MiCA authorisation) with AML/CFT obligations and the travel rule. This is the heaviest part, and it does not depend on the white-paper question.
- **Marketing "the price only rises"** is a misleading-claim problem under MiCA art. 7 and the FSMA's crypto-advertising rules. It is also the clearest possible signal that this is an investment product.
- **Repo constraints it breaks** (README *Binding constraints*):
  - "Non-transferable, off-chain, no peer market."
  - No unit FX / euro price per unit.
  - No published return.

So the sketch as written needs either a prospectus regime or MiCA plus a CASP licence. Each is a six-figure, multi-month project with ongoing compliance. It fails the "keep it simple" goal outright.

## 4. Closest simple version: an off-chain unit with sell-to-cover and a redemption window

Keep the spirit (tax at grant on small amounts, contributors can turn units into euros, price that only ratchets, 10% of revenue funds it) and drop the parts that trigger regulation:

1. **Non-transferable, off-chain ledger units.** They are not transferable, so they are not crypto-assets under MiCA (the art. 3(1)(5) definition requires transferability). They are not negotiable, so they are not transferable securities. They are issued only to contracted contributors for work, so there is no public offer.
2. **Sell-to-cover at grant, done by Refaqt.** As with RSUs, each grant is net-settled: X% in **cash** to cover the tax (contributor chooses 0–50%), the rest in units. No market sale is needed and the price does not move.
3. **Redemption window, yearly or quarterly.** 10% of revenue goes into a redemption reserve. Holders file requests. Requests are filled **pro rata** at the reference price, up to the reserve. The unfilled rest rolls over. The price "never falls" because excess sell pressure **waits in a queue**. Say exactly that, and never call it a guarantee.
4. **Reference price is a formula, ratchet only.** For example, `price_t = max(price_{t−1}, reserve-based formula)`. It is set once per window, not per trade.
5. **Contractual, not promissory.** The terms say redemption is limited to the reserve. Then the liability on the balance sheet is limited to the reserve, not price × supply.

What it costs:

- **It publishes a euro price per unit.** Under the current constraints that is exactly what was banned. The ban only makes sense while tax at grant is avoided. Accepting tax at grant has to be an explicit decision (ADR), checked [as a pair](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md) against option 2 and the bond. Running both side by side would hand the FPS a euro price per hour of work on the option-2 side.
- **Economically it is a contingent, revenue-funded claim**, close to option 2 and the bond. Its only gains are (i) small amounts are taxed early so the contributor has a clean basis, and (ii) partial liquidity before a `P_t` year. The tax at grant is real money that option 2 does not charge.
- **Valuation at grant** must be defensible. Use the formula price, possibly with an illiquidity discount. Do not let a near-zero opening price create a large multiple; start at a sensible formula value (§1, early-mover capture).

## 5. Avoiding an auditor or revisor on every transaction

- A revisor appears only with **shares**: *inbreng in natura* of a receivable, or *inbreng in nijverheid*. Units that are contractual claims, not shares, never trigger a revisor. Avoid any conversion into shares, or batch it yearly (see [2026-11-18 log](2026-11-18_options-convertibles-and-deferred-invoices.md)).
- **Self-billing** (contributor agrees that Refaqt issues the invoice) plus one standard contract annex replaces per-contribution paperwork. The accountant books **one journal entry per period**: grants at the formula price, redemptions paid, outstanding units as a liability up to the reserve.
- The price is set **once per window** by a published formula, so there is no per-trade valuation.
- Statutory audit: a CV/BV needs a commissaris only above the size thresholds. The scheme itself does not add one, unless it becomes a regulated offer (§3), which is the reason to avoid that.
- One DVB prefiling on the unit (box, valuation at grant, deductibility of redemptions) is cheaper than per-transaction comfort. As the README says, a ruling is optional insurance.

## Verdict

- **As written** (transferable token, AMM, "price only rises"): **not recommended.**
  - The no-fall promise contradicts the AMM.
  - The early-grant pump repeats a recorded dead-end.
  - Tax for natural persons is worse than option 2.
  - It falls under prospectus law, or MiCA plus a CASP licence.
- **The §4 variant** is feasible and light on regulation. It mainly decides one question: **do we accept tax at grant in exchange for liquidity?** If yes, write that ADR first, then re-check §4 against option 2 as a pair.

## Open questions

| Question | For |
| --- | --- |
| Accept tax at grant as a design premise (overturns the reason for "no unit FX")? | Founders → ADR |
| Is a non-transferable, redeemable unit with a ratchet formula a debt (bond-like) or a contingent fee for the FPS and in BE GAAP? | Accountant; DVB |
| Deductibility of redemptions above the grant value | DVB; art. 49 / 53, 10° |
| Gain on redemption for a natural person: 10% capital gains tax, *diverse inkomsten*, or professional income? | Counsel; DVB |
| Can §4 coexist with option 2 without publishing a €/hour comparable? | Pair check per mistake 2026-09-14 |

## Sources

- [KPMG — Belgian capital gains tax approved by parliament](https://kpmg.com/be/en/insights/my-tax-compass/corporate-tax-insights/belgian-capital-gains-tax-approved-by-parliament.html)
- [PwC — Circular letter on new Belgian capital gains tax on financial assets](https://news.pwc.be/?p=16639)
- [ESMA — MiCA Article 4, offers to the public of other crypto-assets](https://www.esma.europa.eu/publications-and-data/interactive-single-rulebook/mica/article-4-offers-public-crypto-assets-other)
- [ESMA — MiCA Article 3, definitions](https://www.esma.europa.eu/publications-and-data/interactive-single-rulebook/mica/article-3-definitions)
- [Cerha Hempel — When is a white paper required under MiCAR](https://www.cerhahempel.com/blog/fintech-ledger/when-is-a-white-paper-required-under-micar-applicability-and-exceptions)
