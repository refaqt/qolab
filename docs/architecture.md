# Architecture

QOLAB is a contribution-credit system for work on Refaqt projects. The live design draft lives in [`token-system-design/`](../token-system-design/) while the mechanics are still iterating. **No option is accepted yet.** Vintages are parked (complexity). The cheap-share / option-1 sketch is a **dead-end**. Next pass is option 2 with less machinery.

- Working overview: [token-system-design/architecture.md](../token-system-design/architecture.md)
- Tax and company-law analysis: [token-system-design/token-system.md](../token-system-design/token-system.md)
- Vintage pools (parked): [token-system-design/vintage-pools.md](../token-system-design/vintage-pools.md)
- Cheap-share route (**dead-end**): [token-system-design/cheap-share-route.md](../token-system-design/cheap-share-route.md)
- Spreadsheet for the 2026-09-03 bonding-curve iteration: [token-system-design/2026-09-03_token-system-calculation.ods](../token-system-design/2026-09-03_token-system-calculation.ods)

Stack is not chosen yet. Default is an off-chain ledger.

## Repository layout

| Path | Role |
| --- | --- |
| `.agents/` | Shared agent rules and skills (`refaqt/refaqt-agents` submodule) |
| `doqs/` | Documentation tooling (`refaqt/doqs` submodule) |
| `.agents-local/` | Repo-specific agent rules and skills |
| `docs/` | Living documentation (this pointer, ADRs, log, mistakes) |
| `token-system-design/` | Working token-system draft |
| `AGENTS.md` | Agent entry point |
