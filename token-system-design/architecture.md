# Architecture

System overview and component map for this repository. Update when layout, entry points, or major modules change.

## Purpose

QOLAB is a **contribution-credit system** for work on Refaqt projects. Design is still iterating. **No option is accepted yet.**

Constraints that still bind: non-transferable weights minted with `p = c0 · c^k`; **no** euro quote of `dc/dp` and **no** unit `v = pool / N`; governance membership is separate from the reward; do not mix a dividend story and a fee on the same instrument.

**Parked (complexity):** annual vintage budgets and the time-opened fee cap per lot — [vintage-pools.md](vintage-pools.md). The idle-pool analysis still stands; the packaging is too heavy for now. An effort-tied fee cap is **not** a unit price of `p` — [ADR 2026-09-04](../docs/decisions/2026-09-04_fee-cap-not-unit-price.md).

**Dead-end:** cheap €1 shares whose number tracks `p`, with `p` as a euro dividend cap and burn-on-payout — [cheap-share-route.md](cheap-share-route.md). Rejected: [ADR 2026-09-04](../docs/decisions/2026-09-04_cheap-share-route-dead-end.md).

**Next pass:** option 2 (contingent invoiced fee, points as weights) with **reduced complexity**. Belgian tax and corporate analysis: [token-system.md](token-system.md). Earlier contractor-credit proposal: [docs/decisions/2026-09-02_tax-aware-contribution-credits.md](../docs/decisions/2026-09-02_tax-aware-contribution-credits.md).

## Intended flow (working constraints, payout not decided)

1. Contributor is admitted as a **member** of the CV (governance). Labour is **not** assumed to be volunteer work for tax purposes.
2. Ledger records **contribution points**, then mints weights with `p = c0 · c^k` (early work mints more). No euro quote of `dc/dp`.
3. Weights are **non-transferable**. No peer market.
4. **Do not** pay via extra cheap shares whose count tracks points, and **do not** burn `p` at a euro par. Vintages (budget `P_t`, default-in, time-opened cap, leftover to reserves, no burn for taking the flow) are **parked**, not the live spec.
5. Cash-out box for the next pass is **option 2** (invoiced fee/royalty), not option 1 via labour-quota shares. Those two boxes should not be mixed on the same instrument. Same-year invoices are what avoid stacked VenB under option 2.

Stack is not chosen yet. Default is an off-chain ledger, not a chain.

## Repository layout

| Path | Role |
| --- | --- |
| `.agents/` | Shared agent rules and skills (`refaqt/refaqt-agents` submodule) |
| `doqs/` | Documentation tooling (`refaqt/doqs` submodule) |
| `.agents-local/` | Repo-specific agent rules and skills |
| `docs/` | Living documentation (architecture pointer, ADRs, log, mistakes) |
| `token-system-design/` | Working design: analysis, spreadsheet, this overview |
| `AGENTS.md` | Agent entry point |
