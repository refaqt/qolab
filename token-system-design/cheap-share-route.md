# Cheap-share route (dead-end)

**Status: dead-end.** Do not implement. Do not promise holders this wrapper.

Vintages were parked as too complicated to explain ([vintage-pools.md](vintage-pools.md)). This note is the next sketch: mint `p` from contribution points; `p` is both a **euro cap** on dividends and a **quota** of cheap €1 shares; annual profit is split by shares; every €5,000 received (floor, carried) forces a share sell-back and burns 5,000 `p`.

It is easier to tell. It does **not** survive Belgian tax/company-law facts, and it puts a **euro par on `p`**. Next pass is **option 2** (invoiced contingent fee) with **less machinery** than vintages + time-opened lots — not this.

This is **design input for counsel and an accountant**, not a ruling. Companion tax analysis: [token-system.md](token-system.md).

**Prevention rules applied:** [do not put a euro spot price on certificates](../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not dress labour-quota cheap shares as a dividend](../docs/mistakes/2026-09-04_cheap-share-euro-par.md). Token-engineering: labels do not take compensation outside VAT or income tax; facts beat labels; do not publish a euro par on contribution credits.

---

## Direct answers

| Question | Working answer |
| --- | --- |
| Can a CV issue €1 shares, let contribution points set how many you may buy, pay dividends, and force a sell-down as cash is received? | **On paper, probably yes** (statutes, share class, GA distribution, cooperative withdrawal / own-share rules). Counsel still has to check WVV issuance, equality of members, and whether the real contribution is **inbreng in nijverheid** (art. 1:8 WVV) that must be valued. |
| Can we rely on “no tax at grant, 30% dividend only, no VAT, no RSZ”? | **No.** Share *count* tracks labour. Cash inbreng is €1; economic cap is €5,000 per share. That is the option-1 characterisation the tax note already rejected: allocation that looks like capital, not points. Routing points through cheap shares makes the labour-for-equity facts **louder**, not quieter. |
| Does burning `p` for dividend received put a price on contributions? | **Yes.** 5,000 `p` per €5,000 received is **1 `p` = €1**. Defining `p` as a euro dividend cap already prices the mint; the burn only operates the FX. Same family as the rejected U = €1 peg and `w = dc/dp`. |
| Does this avoid vintage complexity? | The *story* is simpler. The *legal form* is more entangled (shares + `p` + forced buyback + dividends + bonding curve). It also reopens a day-one lifetime euro ceiling and “wait for the fat year” if the GA can retain earnings. |

**Can you implement it like this?** The ledger and statutory sell-down can be written. The legal wrapper “cheap cooperative share, voluntary work, tax only 30% at cash-out” is the part that likely does **not** survive. Treat this document as a **rejected spec**.

---

## How the route worked

Contribution points mint `p` on the bonding curve `p = c0 · c^k` (early work mints more). `p` does two jobs:

1. **Cap** on dividends received over time (remaining `p` ≈ remaining euros).
2. **Weight / quota:** for every 5,000 `p`, the contributor may **buy** one share at **€1** (round up).

Each year, profit the GA distributes is split by **current shares**. For every €5,000 received (floor, remainder carried to later years) the holder **sells one share** (back to the CV) and **burns 5,000 `p`**.

Worked example (year 1, €10,000 profit):

| | Contribution points | `p` minted | Shares (`ceil(p / 5000)`) | Slice of €10,000 | Burn this year |
| --- | ---: | ---: | ---: | ---: | --- |
| Alex | 50,000 | 51,000 | 11 (€11 paid in) | €5,789 | 1 share + 5,000 `p`; carry €789 |
| Bill | 40,000 | 39,000 | 8 (€8 paid in) | €4,211 | 0; carry €4,211 |

After year 1: Alex 46,000 `p` / 10 shares; Bill 39,000 `p` / 8 shares. Lifetime remaining cash is whatever `p` is left. Carry/floor only chunks the same **1:1 par** into €5,000 steps.

If year 1 profit had been €200,000 instead, the day-one cap would bind: Alex takes min(11/19 × €200,000, €51,000) = **€51,000**, then sells down and burns `p`. Bill likewise up to €39,000. Forecasted success → pile in work → extract ~1× points-as-euros immediately. That is the [gold-rush](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md) pattern at ~1× rather than 3×.

---

## Why option 1 does not hold

A Belgian CV’s native tools are **shares**, possibly in classes, issued for cash, with profit rights in the statutes. Cheap €1 membership shares are normal. Forced partial sell-back can be written as statutory redemption. The *form* is closer to option 1 than a free-floating “profit certificate.” The *substance* is still labour-for-equity.

| Intended box | What this route actually looks like |
| --- | --- |
| Dividend (art. 18 WIB 92, 30% WHT, no VAT, no CV deduction) | Number of shares = `f(contribution points)`. *Werkende vennoot* case law wants real capital at risk and profit as return on the joint enterprise, not a points quota. €1 vs a €5,000 cap is not skin in the game. |
| No tax at grant | Right to subscribe a share that can extract €5,000, sold at €1, plus `p` as a €1 lifetime cap. Benefit in kind / consideration for work, with an ascertainable ceiling. Uncertainty of *whether* profit exists still helps; a published remaining-euro cap hurts. |
| VAT (WBTW arts. 22, 26; Tolsma) | Points → `p` → extra shares is a direct link between labour and consideration. Equal-per-member surplus might be a member distribution; this is not that. |
| VVPRbis 18% | There is €1 cash, so someone will ask. Unlikely to stick: labour is the real inbreng; forced redemption after extracting the cap looks like the share was never equity. Do not plan on 18%. |
| Volunteer / cooperative spirit | A profit-distributing CV that pays the same people via a labour-quota share class is deferred pay. Wet 3 juli 2005 is a poor fit. |
| Inbreng in nijverheid done honestly (art. 1:8 WVV) | Shares for a commitment to work must be **valued**. Tax on that value at issuance, then 30% on later dividends, plus lapse/non-compete rules. Often **worse** than a contingent fee. Paying €1 does not turn labour into a cash contribution. |

You still pick **one** tax box. Dividends on shares **and** “this is pay for contributions” on the same instrument is how you get 30% *and* VAT/PIT/RSZ. [token-system.md](token-system.md) §3: putting the right in a share class “still does not stop tax recharacterisation when the number of class-B shares equals contribution points.” This route *is* that mapping.

If it *did* hold as a dividend: VenB at Refaqt first, then 30% WHT — **not** a same-year deductible cost. Pocket math on an already-taxed pool ignores that the same euros as a fee would have reduced VenB.

**Regulatory:** 1 `p` = €1 is the same par-like unit as the old U-token and as `w = dc/dp` (e-money-shaped fact). Off-chain and non-transferable still helps for MiCA. Member-only statutory shares are usually not a public offer; describing this as “buy cheap shares, extract €5,000, sell back” to non-members would look like an investment product.

---

## Why burning `p` prices contributions

Three different “prices” get mixed. This route uses the first two at once.

| Kind | This route | Vintage (parked, not this dead-end) |
| --- | --- | --- |
| **Unit FX** (euros per token) | 5,000 `p` burned per €5,000 → **1 `p` = €1** | No FX. Budget `P_t` split across weights. No burn for taking the vintage. |
| **Ceiling** | Remaining `p` *is* remaining euros. Open in full on day one. | Ceiling is documented effort `E_L`, not minted `p`. Opens at 1×. |
| **Ex-post return** | Always exists after the fact. | Same. |

Belgian VAT and income tax look at ascertainable value, not at the word “cap.” At mint a holder can say: “I received 51,000 `p`, each of which can become €1 of dividend if the GA distributes.” That is a mark-to-market of the *ceiling*. The bonding curve then prices **work in euros**, not only in weight: Alex’s 50,000 points mint a €51,000 cap; Bill’s 40,000 points mint a €39,000 cap.

A fee cap tied to **documented effort** is a different object: it bounds an invoice so the fee stays near the work (art. 49 WIB 92 / arm’s length). It is not a quote of `p`. Here `p` *is* the euro cap, so minting `p` *is* stating the euro value of that contribution’s remaining claim.

Burn-on-payout also reopens stock-model incentives even without an earmarked pot: taking this year’s dividend **shrinks next year’s share count**. If a fat year is visible, holders want the GA to **retain** earnings so they keep shares for the jackpot, then hit the full `p` cap in one go.

~1× of points-as-euros is less of a windfall than a static 3×, but then the instrument is just **deferred pay up to notional**, routed through shares. That is the fee box with extra company-law surface, not a genuine capital return.

---

## What this route was actually doing

It tried to make option 1 *look* true by inserting a €1 share between the points and the cash. The share does not do the economic work; `p` does (weight + euro cap). The €1 is a ticket, not skin in the game.

| Goal | Vintages (parked: too many moving parts) | Cheap-share (dead-end) |
| --- | --- | --- |
| Easy to explain | Weak | Stronger story; weaker legal form |
| No euro quote on the mint | Holds if `P_t / ΣW` is not published | **Fails:** 1 `p` = €1 |
| Option 1 characterisation | Weak (points) | **Weaker** (points → how many shares) |
| Option 2 (deductible fee) | The wrapper that fits a points-minted right | Worse fit: paying a dividend on shares |
| Gold rush / day-one multiple | Time-opened cap was the fix | Full `p` cap open immediately |
| Idle earmarked pot | Solved by flow + default-in | No certificate pot, but GA retention + burn recreates “wait for the fat year” |

---

## Keep / drop

| Keep (still true) | Drop (this route) |
| --- | --- |
| Pick the tax box first. Mixing dividend and fee on one instrument is how you get both levies. | `p` as a euro dividend cap |
| Governance membership (small cash share) **separate** from the reward | Extra profit-sharing shares whose number = `f(points)` |
| Mint `p = c0 · c^k` as a **weight** only, no `dc/dp` in euros | Burn `p` at 1:1 with euros received |
| Non-transferable, off-chain, no peer market | Forced sell-down of cheap shares as the cash-out machine |
| Employees on euro payroll | Volunteer / cooperative-spirit story for a points-minted profit right |
| Option 2: dienstenovereenkomst + contingent invoice | Option 1 via labour-quota shares |

**Rejected as the default** (they reprice labour or camouflage the box):

- Cheap extra shares as the reward vehicle.
- Any 1 `p` = €1 (or 5,000 `p` per €5,000) burn, cap, or par.
- Inbreng in nijverheid as a tax shelter (it is a valuation event).
- VVPRbis on €1 labour-quota shares.

---

## Next iteration (not this note)

Park vintages for **explainability**, not because the idle-pool / no-unit-`v` analysis was wrong. Do not replace them with this dead-end.

Next: **option 2** again — contingent success fee, invoice at cash-out, points as weights — with **reduced complexity** versus lots + time-opened caps + record dates. Constraints that still bind: no euro par on `p`; no unit `v`; do not mix a dividend story on the same instrument; keep the governance share off the reward.

Until counsel and a DVB exist, do not promise holders cheap extra shares, a €1-per-`p` remaining entitlement, or 30% dividend treatment on a points-minted right.
