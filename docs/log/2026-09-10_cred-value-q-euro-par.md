# 2026-09-10 — Cred-weighted euro-par Q (value royalty)

**Role(s):** finance, business-dev

**Status:** **Viable path.** Open. Not accepted as the live spec. No ADR. Does not replace the hours-capped option-2 pass until a later decision. Distinct from [supplier-network Q](2026-09-10_q-token-supplier-network.md) (that Q has **no** euro par and is an access ticket, not a payout). Design input for counsel, not a ruling.

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md) — this fork **accepts** `1 Q = €1` and therefore **accepts** priced consideration (the live option-2 hypothesis tries to avoid that); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md) — no invoice cap is a remaining art. 49 / art. 26 risk, not a reason to call this labour-hours; [do not dress a labour-quota instrument as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md). Token-engineering: labels do not take compensation outside VAT or income tax; facts beat labels. Bitcoin mining is **not** the analogue (identifiable customer).

## What happened

Looked at [SourceCred](https://sourcecred.io/): Cred scores **value added** (graph / PageRank), not hours. Grain is a separate, transferable payout token. Assumed QOLAB can work the same way: contributors are rewarded for the **value** of what they put in, not for logged effort. Contributor BVs exist.

Then simplified away `c` / `p` / effort caps.

### Simple case

A contributor puts a **machine design** on the Refaqt repo. No labour hours. It could have taken five minutes. Others pick it up, improve it, later it is sold. A SourceCred-style algorithm assigns a large Cred score. Each period the revenue pot `P_t` **mints `P_t` Q tokens** with **`1 Q = €1`**. The contributor receives **15,000 Q** and can **invoice Refaqt** (or another settlement). **No cap** for this sketch.

Questions: should the BV invoice to obtain the tokens? Are the tokens consideration for work? If they later rose a lot (20×), would arm’s length bite, or is a success fee out of that test? Is this still “labour”? Is it like mining bitcoin (minters do not invoice hours for datacenters)?

## Working read (viable)

Hours are **irrelevant**. Tax law does not need a timesheet. What it needs is a **customer**.

You contributed a design onto **Refaqt’s** repo. Refaqt (or the network through Refaqt) sells. Refaqt’s pot mints Q at par. You redeem with **Refaqt**. That is **Refaqt paying you €15,000**. `1 Q = €1` plus an invoice means Q is a **coupon for euros**, not a protocol asset with no issuer. Economically you can skip the token and write: “Cred-weighted revenue share: €15,000.”

### Not labour-hours; still a supply to Refaqt

“Labour” in the hours × rate sense is the wrong box. A five-minute design that later carries a product is the same family as a freelance CAD **success fee**, a **royalty** on a drawing, a photographer’s one frame, a songwriter’s royalties. None of those invoices state hours. All of them are still a **supply** (services or IP) to whoever pays.

Belgian VAT (WBTW arts. 22 and 26; Tolsma C-16/93) asks whether there is a **legal relationship** and a **direct link** between what you did and what you received. Both are present: contribution to Refaqt’s repo under a scheme that pays from Refaqt’s pot.

It is **not**:

- a dividend — unless paid *because you are a shareholder*, pro rata to shares. Cred is the opposite of that.
- a gift — a company does not pay €15,000 for a design it sells and have FPS treat it as a present.
- creation of an asset in the void that you later sell on an anonymous market. You redeem Q **with the issuer**, at par, out of **its** turnover.

The precise wrapper among **fee / royalty / sale of IP** is drafting, not a third tax box:

| Wrapper | Typical Belgian result |
| --- | --- |
| Success fee for contributing the design | Professional income in the BV + VAT 21% + deduction at Refaqt if art. 49 holds |
| License: contributor keeps IP, Refaqt pays a revenue share | Same family (royalty/fee). Engineering OSS generally does **not** get the 15% auteursrechten regime |
| Sale of the design to Refaqt | Still a supply; still income in the BV |

You cannot have both “not a dividend” and “not a fee.” Value-based minting makes the **fee / royalty** story stronger, not weaker.

### Invoice (or self-billing)

The contributor **BV invoices Refaqt** when Q is allocated / redeemed — not to “buy” Q as a financial asset, but to document the supply. Description along the lines of: revenue-share / success fee / license — design X — Cred allocation period T. Pool quoted **VAT-exclusive**. Q is burned or cancelled on payment.

Alternatives that stay in the same box: **self-billing** (Refaqt issues the invoice in the BV’s name; common for royalties) or a plain payment. Missing the invoice does not turn this into mining; it only fails VAT invoice hygiene.

Do **not** invoice a nominal €1 for 15,000 Q. That understates consideration. With a hard par, the taxable amount is **€15,000**.

**Timing:** `1 Q = €1` is ascertainable value. FPS can treat income as arising at **allocation of Q**, not at a later invoice. The invoice then settles a voucher already owned. This fork **accepts** that (VAT + VenB in the BV at allocation/invoice). It does **not** try to defer tax until an unpriced cash-out. That is the difference from live option 2 and from the rejected `1 U = €1` sketch, which wanted the par **and** grant-time non-taxation.

### Why this is not Bitcoin mining

Bitcoin miners have **no identifiable customer**. They do not perform a service for an issuer who then owes a fee. EU VAT practice generally treats mining as out of scope for that reason. Income tax still looks at FMV of coins when received. Miners are not asked for datacenter timesheets because **the income is the coins**, not because the activity is invisible.

Here the opposite facts: named company, repo, revenue pot, euro par, invoice to the issuer. The moment the BV invoices Refaqt, the story is already “I supplied something to this company.”

A closer crypto picture than mining: a company issues a token redeemable **1:1 for euros from its own revenue** and gives it to people who put files in its GitHub. That is a voucher / success-fee coupon. Transferable Q at par is also **e-money-shaped**.

### Arm’s length without hours, and without a cap

Dropping hours does **not** drop art. 49 WIB 92 (deduction not excessive) or art. 26 (abnormal advantage). It **changes the comparable**.

Wrong test: “is €15,000 too much for five minutes?”  
Right test: “would an independent have charged about this **for this outcome**?” Typical comparables: a royalty % on sales of machines that use the design; a commission on first commercialisation; what a design bureau would take for a foundational CAD package.

€15,000 for a design that unlocked a much larger pot can be arm’s length. SourceCred is only the **allocation key**. FPS will not care that an algorithm computed it. They will care whether the **result** is a reasonable price for what Refaqt got.

No cap means that test has no internal brake. Cred on a foundational node that keeps paying a large slice of **every** future `P_t` starts to look like a **residual claim on the firm** (equity-like), not like a royalty on *this* design. A royalty on **the products that use the file** is a normal success fee. A royalty on **all Refaqt revenue** because the graph says you are central is the aggressive version — a DVB question, not something “value not labour” puts out of scope.

### If Q later “rose 20×”

Under **this** hypo it cannot: par is €1. Upside is **more Q** when Cred is high and `P_t` is large, not Q appreciating.

A 20× would need a **different** instrument (transferable unpegged token, phantom priced by the GA, issuer put). Then:

- Third party pays 20× → not extra consideration **from Refaqt**; the BV still has VenB on the gain; needs a market (MiCA / grant-time FMV).
- Refaqt redeems or buys back at 20× → extra consideration from Refaqt; art. 49 / art. 26 fully on. A “success fee” label is the argument you file, not an exemption.

[Tokens-not-shares log](2026-09-10_tokens-not-shares-avoid-revisor.md): a success-fee label does not switch off arm’s length.

### Two different Q sketches

| | This path (viable) | [Supplier-network Q](2026-09-10_q-token-supplier-network.md) (open) |
| --- | --- | --- |
| What Q is | Coupon for euros from `P_t` | Access ticket to place supplier orders |
| Par | **`1 Q = €1`** | No par; suppliers paid in fiat |
| Split | SourceCred / value (Cred) | Was sketched as a stream to `p`-holders |
| How you cash | Invoice / self-bill Refaqt | Use Q to order, or (risky) sell to builders |
| Hours | Not used | Not the point of that sketch either |
| Tax posture | **Accepts** priced consideration | Tries to stay an unpriced permission if non-transferable |

Do not mix them under one letter Q in a spec without renaming.

## How it would work (simple case)

1. **Contract up front** (dienstenovereenkomst or IP license + Cred annex): opt into Q; Cred-weighted share of each euro pot; Q redeemable with Refaqt; `1 Q = €1` is delayed euros.
2. Design is contributed. **No timesheet.** Cred is computed (SourceCred or otherwise). That is governance of the split, not the tax box.
3. A pot exists (example: €100,000). 100,000 Q minted. Contributor receives 15,000 Q.
4. The **BV invoices €15,000** (VAT extra if the supply is taxable). Refaqt pays; Q cancelled. Refaqt books a cost; the BV books turnover.
5. Repeat when later pots run. No effort cap in this sketch; arm’s length stays a **royalty/value** test.

## Decisions

None as ADR. Record as a **viable path**:

- Value / Cred as the split key, **not** hours, is a coherent option-2 (fee / royalty) story when the payer is Refaqt.
- `1 Q = €1` minted from `P_t`, Cred-weighted, redeemed by **invoice or self-billing**, is mechanically a euro revenue share. The token is packaging.
- This path **accepts** VAT and professional income / VenB at allocation of Q. It does not pursue grant-time deferral.
- The Bitcoin-mining analogy **does not apply** (identifiable customer; invoice to the issuer).
- No hours cap does **not** remove art. 49 / art. 26. The comparable is outcome / royalty, not minutes. An uncapped share of **all** future `P_t` remains the aggressive end.
- Does **not** accept this as the live spec. Does **not** unpark vintages. Does **not** revive cheap-share or bonding-curve shares. Does **not** merge this Q with supplier-network Q. Does **not** treat 20× appreciation of a par token as a feature of this path.

## Open Questions

- Counsel / DVB: characterise the €15,000 as a contractual success fee or IP royalty; confirm **not** a dividend when the key is Cred.
- Time of supply: allocation of Q vs invoice, given the published par (WBTW arts. 22, 26).
- Art. 49: is an **uncapped** Cred share of each `P_t` still a deductible royalty, or must the royalty be scoped to products that use the contributor’s design?
- Self-billing vs contributor-issued invoice; what if the “contributor” is a natural person without a BV.
- Cred algorithm as allocation key: who may change weights; dispute process; whether a GA override looks like a discretionary bonus.
- Transferability of Q: issuer-only vs peer market (e-money / MiCA if transferable at par).
- How this sits next to live option 2 (hours cap, unpriced `p`) — **replace** for design contributions, sit **beside** (designs on Cred+Q, time-based work still option 2), or drop.
- Rename one of the two Q sketches before a spec draft.

## Next Steps

- Keep this as a viable-path log; do not treat it as the live spec.
- If pursued: draft the license / dienstenovereenkomst + Cred annex with a worked number (15,000 Q, year with `P_t = 0`, year with a large foundational Cred share); file with DVB.
- Do not promise that “it is not labour so there is no VAT.” Do not promise that “success fee” removes arm’s length. Do not publish a 20× or ROI on Q.
- Do not confuse this euro-par Q with [supplier-network Q](2026-09-10_q-token-supplier-network.md).
