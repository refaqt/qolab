# Architecture

QOLAB is a contribution-credit system for work on Refaqt projects. The live design draft lives in [`token-system-design/`](../token-system-design/) while the mechanics are still iterating. **No option is accepted yet.** Vintages are parked (complexity). Cheap-share and bonding-curve shares (cheap grant value + revenue mint) are **dead-ends**. Next pass is option 2 with less machinery. **Accepted:** amortize `p` against remaining opened cap ([p-burn-remaining-cap.md](../token-system-design/p-burn-remaining-cap.md)); nested mint budgets ([nested-mint-budgets.md](../token-system-design/nested-mint-budgets.md)); project-as-contractor cash path ([ADR 2026-09-09](decisions/2026-09-09_project-as-contractor.md)).

- Working overview: [token-system-design/architecture.md](../token-system-design/architecture.md)
- Tax and company-law analysis: [token-system-design/token-system.md](../token-system-design/token-system.md)
- DVB questions **(a)–(p)** (filing catalog): [token-system-design/dvb-questions.md](../token-system-design/dvb-questions.md)
- `P_t` / cap-opening discussion (lots, year-1 1×, path to 10×): [docs/log/2026-09-10_pt-distribution-and-cap-opening.md](log/2026-09-10_pt-distribution-and-cap-opening.md)
- Q-token for supplier-network access (**open**, not live spec): `p` distributes Q minted from OSS designs/tools; Q gates supplier orders (not fiat payment) — [docs/log/2026-09-10_q-token-supplier-network.md](log/2026-09-10_q-token-supplier-network.md)
- Cred-weighted euro-par Q (**viable path**, not live spec): SourceCred-style value split; `P_t` mints `P_t` Q at `1 Q = €1`; contributor BV invoices / self-bills; no hours; fee/royalty not mining; accepts priced consideration — [docs/log/2026-09-10_cred-value-q-euro-par.md](log/2026-09-10_cred-value-q-euro-par.md)
- Tokens instead of shares to skip the inbreng-revisor (**open**, not live spec): phantom / revenue-share / profit-share contracts vs NV *winstbewijzen*; arm’s length; warrants; 10× of labour is not a dividend FPS will ignore — two instruments (fee + cash shares) or gated option-2 10× — [docs/log/2026-09-10_tokens-not-shares-avoid-revisor.md](log/2026-09-10_tokens-not-shares-avoid-revisor.md)
- Vintage pools (parked): [token-system-design/vintage-pools.md](../token-system-design/vintage-pools.md)
- Why an effort fee cap is not a unit price of `p`: [docs/decisions/2026-09-04_fee-cap-not-unit-price.md](decisions/2026-09-04_fee-cap-not-unit-price.md)
- Option-2 personal effort cap (working sketch): [docs/log/2026-09-04_option-2-effort-cap.md](log/2026-09-04_option-2-effort-cap.md)
- Proportional burn of `p` against remaining opened cap (**accepted**): [token-system-design/p-burn-remaining-cap.md](../token-system-design/p-burn-remaining-cap.md), [ADR 2026-09-08](decisions/2026-09-08_p-burn-remaining-cap.md)
- Nested mint budgets for sub-projects (**accepted** mint gate): [token-system-design/nested-mint-budgets.md](../token-system-design/nested-mint-budgets.md), [ADR 2026-09-08](decisions/2026-09-08_nested-mint-budgets.md). Cash path (**accepted**): the project entity holds root `p` and invoices `P_t`; euros land in a subpool and are split by `p_j` — [ADR 2026-09-09](decisions/2026-09-09_project-as-contractor.md), [2026-09-09 log](log/2026-09-09_hours-cap-and-project-contractor.md). Direction A (distribute parent `p` to people) is not the live model.
- Option-2 sketch that burns `S` against euros (**not** the next pass): [docs/log/2026-09-07_s-burn-euro-par.md](log/2026-09-07_s-burn-euro-par.md)
- Cheap-share route (**dead-end**): [token-system-design/cheap-share-route.md](../token-system-design/cheap-share-route.md). A 2026-09-08 variant (€0.10 vs €10, quota = `f(p)`, no burn) is the same rejection: [docs/log/2026-09-08_option-1-tenth-vs-ten-euro-shares.md](log/2026-09-08_option-1-tenth-vs-ten-euro-shares.md). 2026-09-10 variants (no investors / informal; MoU → unpaid / “given” / revalued class if `N = f(work)`) are the same rejection: [docs/log/2026-09-10_no-investors-euro-shares.md](log/2026-09-10_no-investors-euro-shares.md), [docs/log/2026-09-10_startup-equity-mou.md](log/2026-09-10_startup-equity-mou.md)
- Bonding-curve shares with cheap grant value (**dead-end**): [docs/log/2026-09-07_bonding-curve-shares-dead-end.md](log/2026-09-07_bonding-curve-shares-dead-end.md)
- Spreadsheet for the 2026-09-03 bonding-curve iteration: [token-system-design/2026-09-03_token-system-calculation.ods](../token-system-design/2026-09-03_token-system-calculation.ods)
- Spreadsheet for the 2026-09-07 bonding-curve shares dead-end: [token-system-design/2026-09-07_token-system-calculation.ods](../token-system-design/2026-09-07_token-system-calculation.ods)

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
