# Supplier-network access token (open)

**Status: open.** A fork in which weights `p` do **not** give a slice of the euro pool `P_t` but a stream of a new token that gates transactions in the Refaqt supplier network. Not accepted; no ADR; not the live spec. Design input, not a ruling.

Source: [2026-09-10 Q-token for supplier-network access](../../../docs/log/2026-09-10_q-token-supplier-network.md). **Naming:** that log and the [euro-par Cred Q](../scoped-royalty-cred-q/README.md) use the same letter for two different objects. Proposal on the record: the euro-par coupon keeps “Q”; this access token gets another name before any spec draft. Until then this page says “access token.”

**Prevention rules applied:** [no euro spot price on a growing pool](../../../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [remaining `p` is not remaining euros](../../../docs/mistakes/2026-09-04_cheap-share-euro-par.md); a peer market prints a euro price ([S-burn log](../../../docs/log/2026-09-07_s-burn-euro-par.md)).

---

## The idea

- The access token is minted every period from open-source hardware designs and tools (mint mechanism to be designed) and distributed to `p`-holders.
- It is **required to place orders** with suppliers through the network (specs, order processing, invoicing into accounting). Suppliers are still paid in **fiat**; the token is not payment.
- Builders who need it can contribute to earn it.

## Working read (not a decision)

| Question | Working answer |
| --- | --- |
| Is a closed-loop, non-transferable access token still an asset? | Not e-money (no par; suppliers paid in fiat). Still an **economic good** if it is a fungible balance you need and minting is not free — a ticket to a service, not a login. A personal, expiring **right to use** the ordering system (SaaS access) would not be a token asset; a balance is. |
| Does `p` → a stream of tokens price `p`? | `p` becomes a yield-bearing right whose coupon is the token. Belgian tax can still see consideration; “no public price” helps but does not wipe use-value for builders. |
| What if non-builders sell their tokens to builders? | That is a market; it prints a euro price FPS can copy onto later mints, and `p` inherits it (PV of expected mint × €/token). Same fact as transferable `S`. |
| Does “no cap” or a time-burn of `p` remove the euro value? | No. Uncapped easy mint drives the price to ~0 and the token stops gating; scarce mint keeps it valuable. Time-burn shortens the claim; it does not unprice each drop. |
| Stranded tokens | The tell: if the only way non-builders get value is to sell to builders, that **is** a market in the token. |

Closer-to-unpriced fork: a personal, expiring **right to use** the ordering system, not a fungible balance paid out to `p`.

## Open questions

- Mint mechanism from OSS designs / tools.
- Closed-loop, non-transferable token as consideration at grant.
- Selling unused tokens to builders: tax, MiCA/FSMA, pricing of `p`.
- Relation to live option 2: replace the euro pool, sit beside it, or neither.
- Other uses of the token besides supplier-network access.
- Name.

## Next steps

- Keep open; do not treat as the live spec.
- If pursued: DVB on the token as access ticket vs priced token, and on `p` as a claim on a token stream. No peer market without revisiting the S-burn finding.
