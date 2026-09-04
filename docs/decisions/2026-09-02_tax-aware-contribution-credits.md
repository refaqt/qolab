# ADR — Tax-aware contribution credits (Belgium)

- **Date:** 2026-09-02
- **Status:** Proposed. Payout packaging: vintages [parked](2026-09-04_cheap-share-route-dead-end.md) (complexity); cheap-share option-1 wrapper [rejected](2026-09-04_cheap-share-route-dead-end.md). Next pass is simpler option 2.

## Context

QOLAB is meant to reward Refaqt contributions when there is revenue, cap those rewards, pay more than hours × rate when Refaqt does well, and avoid VAT and income tax at grant while credits have no cash value.

The first mechanics sketch used C-tokens, a power-law bonding curve, R-tokens, and U-tokens at 1 U = 1 euro, with a 10% revenue pool and peer transfers. Under Belgian VAT (arts. 22, 22bis, 26 WBTW) and income-tax practice (tax at vesting/disposal, not at euro conversion), that sketch creates an ascertainable value at grant. Peer transfer and a euro peg also pull in e-money / FSMA / MiCA analysis. The “1 U = 1 euro” label also contradicts the pro-rata pool formula, which does not pay par.

Full analysis of that sketch lived in `docs/token-system.md` (moved). Current iteration: [token-system-design/token-system.md](../../token-system-design/token-system.md).

## Decision

Until counsel and an accountant (and preferably a DVB ruling) say otherwise, design QOLAB as follows:

1. **One instrument:** non-transferable **contribution weights** (not C / R / U, not a euro peg).
2. **Mint function** may be a power-law or vintage multiplier so early work gets more weight. It must **not** be quoted as a euro price.
3. **No secondary market.** Transfers only to treasury, on death, or to a successor vehicle of the same beneficial owner.
4. **Cash only in distribution rounds** funded from a solvency-checked pool (`min` of a profit metric, an optional revenue cap, and available cash) — not an automatic 10% of turnover. Do **not** use `v = pool / N`. Vintage packaging (default-in, leftover to reserves, time-opened lot cap) is **parked** for complexity — [ADR 2026-09-03](2026-09-03_vintage-pools-no-unit-price.md), [ADR 2026-09-04](2026-09-04_cheap-share-route-dead-end.md). Next pass is simpler option 2, not cheap extra shares.
5. **Fee cap** at payout should stay tied to **documented effort**, not to a euro par on minted `p`. The time-opened per-lot formula is parked with vintages: [ADR 2026-09-03 time-opened fee cap](2026-09-03_time-opened-fee-cap.md).
6. **Invoice at payout** is the consideration. Pool amounts are **VAT-exclusive**. Credits are contractually a contingent success fee, not shares and not a dividend. Labour-quota €1 shares as a dividend wrapper is a **dead-end** ([cheap-share-route.md](../../token-system-design/cheap-share-route.md)).
7. **Membership is optional and separate.** Statutes must say credits are not parts/shares and cash-out is not a distribution on capital (especially if the CV is or becomes a social enterprise). Do not issue extra profit-sharing shares whose number tracks contribution points.
8. **Relationship-appropriate contracts:** employment (euro salary) vs dienstenovereenkomst + IP/CLA + QOLAB annex. Off-chain ledger by default.

## Consequences

- Goals 1–4 remain reachable without publishing a token price.
- VAT and PIT **should** attach at invoice, not at grant — this is a hypothesis for DVB, not a guarantee.
- Contributors who wanted to sell credits to each other cannot; liquidity is only via Refaqt rounds.
- Refaqt must run round administration, invoicing, and contractor-vs-employee hygiene.
- Implementation can stay a database; no chain, no white paper.
- Next step is a simpler option-2 spec (less machinery than vintage lots), then human review (tax, corporate, social). Do not draft regulation around cheap extra shares.
