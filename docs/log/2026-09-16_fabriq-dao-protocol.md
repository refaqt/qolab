# 2026-09-16 — Fabriq DAO to run the manufacturing protocol (open)

**Role(s):** business-dev, finance

**Status:** Open sketch. Not accepted. No ADR. Not a new path folder. Closest existing path: [supplier-network access token](../../token-system-design/paths/q-supplier-access/README.md) ([2026-09-10 log](2026-09-10_q-token-supplier-network.md)).

**Prevention rules applied:** [mission as a design constraint](../mission.md) — a price-rise story is not enough on its own; [do not put a euro spot price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); a peer market prints a euro price ([S-burn log](2026-09-07_s-burn-euro-par.md)); [a second instrument must not publish the comparable](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md). The letter Q already names two different tokens ([access token](2026-09-10_q-token-supplier-network.md) vs [euro-par Cred Q](2026-09-10_cred-value-q-euro-par.md)).

## What happened

Recorded a future idea: build **Fabriq DAO**. A DAO is a member-run organisation on a protocol (rules in software, not only in a company). The sketch is about the manufacturing network, not about changing the live option-2 fee.

### The idea

- Put finance through **Fabriq DAO**, not through Refaqt. Refaqt would not be the pipe for all money.
- The DAO **manages the protocol** (the shared rules and software for the network).
- The protocol **requires a Q-token**. Demand for that token is meant to raise its price.
- Actions that would need the Q-token:
  - create and update a product data file (Digital Product Passport, **DPP**);
  - receive requests for quotes (**RFQs**) and orders;
  - be listed as a commercial party.
- What stops others from copying this with no paywall, or with a different paywall: **network effect**. The protocol only sends RFQs to the network. The DPP only connects a product to potential suppliers **in** the network.
- How to start:
  1. Form **Fabriq LLC** (a limited company, or a later legal form) that governs Fabriq.
  2. Refaqt buys **DAI** (a dollar-pegged digital cash token) and uses it to buy **Q**.
  3. Q is paid to the protocol. Refaqt gets a **receipt**.

### Working read (not a decision)

This is the same family as the [2026-09-10 access-token sketch](2026-09-10_q-token-supplier-network.md): a token gates use of the supplier network; suppliers are still paid in ordinary money. This sketch adds three things: (1) DPP create/update and a commercial listing, not only placing orders; (2) a separate Fabriq entity so finance does not all flow through Refaqt; (3) an explicit start path (LLC, DAI → Q, receipt).

The mission can support a shared protocol that helps local, on-demand manufacturing. “The Q-token price will increase” is **not** a mission story. If that is the only reason to require Q, the sketch fails the [mission constraint](../mission.md). A receipt for Q spent on protocol use can be a real cost of a service. A plan to hold Q so the price rises is a different fact: then Q has a spot price, and a peer book prints a euro (or dollar) value that tax authorities can copy. Same finding as selling the access token to builders.

The letter Q already names two different tokens in this repo: the access ticket and the euro-par Cred coupon. This sketch uses Q for the access ticket. Rename before any spec draft.

Fabriq LLC / DAO next to Refaqt is a **second instrument** (or a second company). Before it is specified, list what the Refaqt contributor fee and the investor bond rely on being **absent**, and check that Fabriq does not supply those facts in a document anyone must publish.

Network effect is a reason users stay. It is not a legal barrier. Others can still run a free protocol. The claim is that RFQs and DPP links only reach this network, so a copy without the network is less useful.

## Decisions

None. Sketch stays **open**. Not an ADR. Does not replace option 2. Does not accept a market in Q. Does not add a path folder (log only).

## Open Questions

- Rename vs the two existing Q’s before any spec draft.
- Does moving finance to Fabriq change option 2, the capped bond, or QOLAB at all, or does it sit beside them?
- Pair check: what facts do the Refaqt instruments need to stay absent, and does a priced Q or a DAI→Q purchase print them?
- Closed-loop ticket vs transferable token: tax, MiCA/FSMA, and whether “price will increase” is even the goal.
- Why an LLC (often a US form) rather than a Belgian CV or another form, and who holds it before a DAO exists.
- What the receipt is for (service cost, token purchase, or both), and in which books it lands.
- Is network effect enough of a moat if a rival sends RFQs with no token gate?

## Next Steps

- Keep the sketch in the log. Do not treat Fabriq DAO as the live spec.
- If this path is pursued: add a row on the [path map](../../token-system-design/README.md) **before** a folder, run the pair check, and take the access-token tax questions (ticket vs priced token) with it.
- Do not add a peer market in Q without revisiting [peer market prints a euro price](2026-09-07_s-burn-euro-par.md).
