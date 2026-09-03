# Architecture

System overview and component map for this repository. Update when layout, entry points, or major modules change.

## Purpose

QOLAB is a **contribution-credit system** for work on Refaqt projects. The working iteration rewards documented contribution with non-transferable **weights** minted on a bonding curve, and pays them from **annual vintage budgets** — not from a unit price `v = pool / certificates`.

Belgian tax and corporate analysis: [token-system.md](token-system.md). Idle-pool / wait-and-run problem and vintage replacement: [vintage-pools.md](vintage-pools.md). Earlier contractor-credit proposal: [docs/decisions/2026-09-02_tax-aware-contribution-credits.md](../docs/decisions/2026-09-02_tax-aware-contribution-credits.md). Proposed vintage ADR: [docs/decisions/2026-09-03_vintage-pools-no-unit-price.md](../docs/decisions/2026-09-03_vintage-pools-no-unit-price.md). **No option is accepted yet** — design is still iterating.

## Intended flow (working, not decided)

1. Contributor is admitted as a **member** of the CV (governance). Labour is **not** assumed to be volunteer work for tax purposes.
2. Ledger records **contribution points**, then mints weights with `p = c0 · c^k` (early work mints more). No euro quote of `dc/dp`.
3. Weights are **non-transferable**. No peer market.
4. Each year the GA/board sets a **vintage budget** `P_t` (waterfall + solvency). Default-in split across weights; leftover to reserves; weights are not burned for taking the vintage. No `v = pool / N`.
5. Cash-out is either a **dividend** (option 1) or an **invoiced fee/royalty** (option 2). Those two boxes should not be mixed on the same instrument. Same-year invoices are what avoid stacked VenB under option 2.

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
