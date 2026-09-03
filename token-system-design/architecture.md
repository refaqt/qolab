# Architecture

System overview and component map for this repository. Update when layout, entry points, or major modules change.

## Purpose

QOLAB is a **contribution-credit system** for work on Refaqt projects. The 2026-09-03 iteration rewards documented contribution with non-transferable **profit certificates** minted on a bonding curve, cashed from a GA-set pool, and burned on withdrawal.

Belgian tax and corporate analysis of that iteration: [token-system.md](token-system.md). Earlier contractor-credit proposal: [docs/decisions/2026-09-02_tax-aware-contribution-credits.md](../docs/decisions/2026-09-02_tax-aware-contribution-credits.md). **No option is accepted yet** — design is still iterating.

## Intended flow (working, not decided)

1. Contributor is admitted as a **member** of the CV (governance). Labour is **not** assumed to be volunteer work for tax purposes.
2. Ledger records **contribution points**, then mints certificates with `p = c0 · c^k` (early work mints more).
3. Certificates are **non-transferable**. No peer market.
4. The GA sets a **profit (or revenue) pool**. Withdrawal uses a payout-time conversion, not a published euro rate at mint — see the analysis.
5. Cash-out is either a **dividend** (option 1) or an **invoiced fee/royalty** (option 2). Those two boxes should not be mixed on the same instrument.

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
