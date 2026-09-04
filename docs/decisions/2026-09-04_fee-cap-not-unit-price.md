# ADR — Effort fee cap is not a unit price of `p`

- **Date:** 2026-09-04
- **Status:** Proposed
- **Amends:** [2026-09-02](2026-09-02_tax-aware-contribution-credits.md) point 5 (fee cap tied to documented effort). Clarifies the parked vintage note and applies to the **next option-2 pass**.
- **Does not unpark** vintages. Does not revive cheap-share.

## Context

The vintage flow (annual budget `P_t` split by share of `p`, invoice clipped by a multiple of documented effort) looks as if it implies

`€/p = (k × hourly rate × hours) / Δp`.

If that quotient were a grant-time unit price, VAT and income tax would attach at mint — the failure mode the tax analysis already rejected for `w = dc/dp`, `v = pool / N`, and 1 `p` = €1.

Full argument: [token-system-design/vintage-pools.md](../../token-system-design/vintage-pools.md) (“Does `(k × hours × rate) / Δp` price `p`?”).

## Decision

Until counsel and an accountant (and preferably a DVB ruling) say otherwise:

1. A fee cap on **documented effort** `E_L` (hours × frozen contractor band, or a task estimate) is an **invoice ceiling**, not a unit FX of `p`. The next option-2 spec may keep such a cap.
2. **Do not** treat `(k × E_L) / Δp` as the price of `p`. Do not publish it at mint. Do not book the cap as a receivable.
3. What *does* price the mint, and stays rejected: a published €/unit (`w`, `v = P/N`), remaining `p` as remaining euros, or choosing a denominator so holders hit a target on points.
4. Ask DVB item **(i)** explicitly: effort-tied fee cap versus implied `€/p` at grant.

## Consequences

- The reconstruction “`P_t` split by share of `p`, never more than `k × E`” can be true without putting a euro par on `p`.
- Same work, different mint dates, same cap, different `Δp`: the quotient is not a property of `p`.
- A ceiling is not consideration “to be received” (WBTW art. 26) while `P_t` may be zero. This remains a **hypothesis**, not a ruling.
- A static `k×` open on day one plus a forecasted fat pool still looks more like ascertainable value — that is a separate reason the parked design opened at 1×, and it still binds a simpler option-2 cap: do not make the long-risk multiple a near-certain payday at grant.
