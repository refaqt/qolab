# 2026-09-10 — Q-token for supplier-network access (open)

**Role(s):** finance, business-dev

**Status:** Open. Not accepted. Not the live option-2 pass. No ADR.

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not treat remaining `p` as remaining euros](../mistakes/2026-09-04_cheap-share-euro-par.md); a peer market prints a euro price ([S-burn log](2026-09-07_s-burn-euro-par.md)). Token-engineering: labels do not take compensation outside VAT or income tax; facts beat labels.

## What happened

Sketched a fork where weights `p` do **not** give a right to a slice of the euro revenue pool `P_t`. Instead `p` gives a right to an amount of a new token **Q**.

### The idea

- Q is minted from **open-source hardware designs and open-source tools** that are created (minting mechanism still to figure out).
- Those OSS assets mint Q **every period**. That Q is **distributed to p-holders**.
- Q is used to **establish transactions in the supplier network**. Example: someone wants to build a machine and place orders with suppliers immediately — Q is required to place those orders.
- Q is **not** for paying the suppliers. Suppliers still get paid in **fiat** in the normal way. Q is for making the transaction smooth (supplier gets the right specs, everything is put in a database, orders can be automatically processed, invoices automatically go to the accounting system, etc.). This is **one** of the uses of Q.
- People that want to build machines therefore need Q. They could contribute themselves to obtain Q through the minting.

Questions kept open:

1. Would Q in this case **not** be an asset?
2. Other contributors are left with Q they cannot use. One option: **sell Q to machine builders**. That creates a market and thus a euro value for Q. How does that change things?
3. If there is **no cap** on how much Q you can obtain, would that still provide a euro value to `p` as well?
4. If `p` would **automatically get burned with time**, would that still give a euro value to `p`?

### Working read (not a decision)

Closed-loop Q, no sales: not e-money (no par, suppliers paid in fiat). Still an **economic good** if Q is a fungible balance you hold, you need it to place an order, and minting is not free. That is a ticket to a service (network coordination), not a login. A personal, non-transferable, expiring permission would not be a token asset; a Q balance is. `p` claiming a **stream** of Q from OSS assets that mint every period is a yield-bearing right whose coupon is Q. Belgian tax: `p` → Q can still be consideration; no public price helps, it does not wipe use-value for builders. Non-builders who cannot transfer Q have a stronger “stranded, no value to me” argument — which is why the sale option appears. MiCA: issuer-only / off-chain / non-transferable can stay outside; that is “not a crypto-asset,” not “not an asset.”

Selling Q to builders: a members-only book is enough. Same fact as transferable `S` ([2026-09-07 S-burn](2026-09-07_s-burn-euro-par.md)): a peer market **prints a euro price**; FPS can copy it onto later mints. Then Q has a spot €/Q (grant of Q is priced consideration). `p` becomes a claim on a stream of priced Q (grant-time value ≈ discounted expected Q-mint × €/Q). The euro quote moved off `P_t` onto Q; `p` inherits it. “Builders could contribute instead” sets a ceiling on €/Q (cost in time of minting); it does not remove the price.

No cap on how much Q you can obtain: does **not** by itself strip euro value off `p`. It does so only if supply of Q swamps demand (orders × Q burned per order). Uncapped easy mint → €/Q → ~0 and Q stops gating. Scarce mint (hard designs, high Q per order) → Q stays valuable → `p` still has share of mint × €/Q. Designs that keep minting every period are a growing coupon stream (same class of fact as a unit price on a growing stock).

Time-burn of `p`: if Q is priced, `p` still has euro value = PV of remaining Q drops × €/Q. Burn shortens the claim (less “hold forever”); it does not unprice each drop or stop income at each Q distribution if Q is marketable.

Stranded Q is the tell: if the only way non-builders get value is to sell to builders, that **is** a market in Q, and then `p` is a claim on that market. Capping Q or burning `p` over time changes **how much** that claim is worth, not **whether** it is a euro-valued asset.

Fork that would stay closer to unpriced: personal, expiring **right to use** the ordering system (SaaS access), not a fungible Q balance paid out to `p`.

## Decisions

None. Sketch stays **open**. Not an ADR. Does not replace option 2. Does not unpark vintages. Does not accept a Q market.

## Open Questions

- Minting mechanism for Q from OSS designs/tools.
- Would closed-loop, non-transferable Q (needed to order, not to pay suppliers) still be an asset / consideration at grant?
- If unused Q is sold to machine builders: tax, MiCA/FSMA, and whether that prices `p`.
- No cap on Q obtained: does `p` still get a euro value, or only if Q stays scarce vs order-flow?
- Automatic time-burn of `p`: does that still leave a euro value on remaining `p` if Q is priced?
- How Q relates to live option 2 (`P_t` invoices, effort cap) — replace the euro pool, sit beside it, or neither?
- Other uses of Q besides supplier-network access.

## Next Steps

- Keep the sketch open; do not treat Q as the live spec.
- If this path is pursued: DVB on Q as access ticket vs priced token, and on `p` as a claim on a Q stream.
- Do not add a peer market in Q without revisiting [peer market prints a euro price](2026-09-07_s-burn-euro-par.md).
