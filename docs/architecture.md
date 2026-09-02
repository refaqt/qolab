# Architecture

System overview and component map for this repository. Update when layout, entry points, or major modules change.

## Purpose

QOLAB is a **contribution-credit system** for work on Refaqt projects. It is meant to reward documented contributions when Refaqt has revenue, cap those rewards, and let successful years pay more than hours × rate — without treating credits as shares or as a tradable coin.

Belgian tax and corporate analysis of the first token sketch, and the proposed credit design: [docs/token-system.md](token-system.md). Proposed decision: [docs/decisions/2026-09-02_tax-aware-contribution-credits.md](decisions/2026-09-02_tax-aware-contribution-credits.md).

## Intended flow (proposed)

1. Contributor supplies work under a services contract (or is an employee paid in euro).
2. Ledger records **non-transferable weights** from effort, with an early-bird mint factor.
3. When a distribution round opens, opted-in weights share a solvency-checked euro pool, each person capped at a multiple of documented effort.
4. Payment follows an invoice (VAT-exclusive). That invoice is the taxable consideration.

Stack is not chosen yet. Default is an off-chain ledger, not a chain.

## Repository layout

| Path | Role |
| ---- | ---- |
| `.agents/` | Shared agent rules and skills (`refaqt/refaqt-agents` submodule) |
| `doqs/` | Documentation tooling (`refaqt/doqs` submodule) |
| `.agents-local/` | Repo-specific agent rules and skills |
| `docs/` | Living documentation (architecture, ADRs, log, mistakes) |
| `docs/token-system.md` | Belgian tax/legal analysis and target mechanics |
| `AGENTS.md` | Agent entry point |
