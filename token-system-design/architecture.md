# Architecture

System overview and component map for this repository. Update when layout, entry points, or major modules change.

## Purpose

QOLAB is a **contribution-credit system** for work on Refaqt projects. Design is still iterating. **No option is accepted yet.**

Constraints that still bind: non-transferable weights minted with `p = c0 · c^k`; **no** euro quote of `dc/dp` and **no** unit `v = pool / N`; governance membership is separate from the reward; do not mix a dividend story and a fee on the same instrument.

**FX** in these notes means a conversion rate between two units (as in foreign exchange), typically euros per token (`€/p`). A **unit FX** is a published rate that turns every outstanding token into euros the same way at a given date. The live spec does not use one.

**Parked (complexity):** annual vintage budgets and the time-opened fee cap per lot — [vintage-pools.md](vintage-pools.md). The idle-pool analysis still stands; the packaging is too heavy for now. An effort-tied fee cap is **not** a unit price of `p` — [ADR 2026-09-04](../docs/decisions/2026-09-04_fee-cap-not-unit-price.md).

**Dead-ends:** cheap €1 shares whose number tracks `p`, with `p` as a euro dividend cap and burn-on-payout — [cheap-share-route.md](cheap-share-route.md), rejected [ADR 2026-09-04](../docs/decisions/2026-09-04_cheap-share-route-dead-end.md). The same rejection covers a 2026-09-08 variant (€0.10 contributor shares vs €10 investor shares, quota = `f(p)`, dividend per share, no burn) — [docs/log/2026-09-08_option-1-tenth-vs-ten-euro-shares.md](../docs/log/2026-09-08_option-1-tenth-vs-ten-euro-shares.md). Steep bonding-curve shares with a cheap constant contribution value (€0.01/point) and revenue minting on the same curve — [docs/log/2026-09-07_bonding-curve-shares-dead-end.md](../docs/log/2026-09-07_bonding-curve-shares-dead-end.md), spreadsheet [2026-09-07_token-system-calculation.ods](2026-09-07_token-system-calculation.ods), rejected [ADR 2026-09-07](../docs/decisions/2026-09-07_bonding-curve-shares-dead-end.md).

**Accepted (payout weight):** amortize `p` against remaining opened cap each vintage: `burned_i = p_i · (alloc_i / rem_i)`; `rem = 0` ⇒ `p = 0`. Not a euro par. [p-burn-remaining-cap.md](p-burn-remaining-cap.md), [ADR 2026-09-08](../docs/decisions/2026-09-08_p-burn-remaining-cap.md).

**Accepted (sub-projects, mint gate):** nested mint budgets — unofficial work does not move parent `c`; parent gates a stream of root `p`. [nested-mint-budgets.md](nested-mint-budgets.md), [ADR 2026-09-08](../docs/decisions/2026-09-08_nested-mint-budgets.md).

**Accepted (sub-projects, cash path):** the **project entity** holds that root `p` and invoices `P_t` like a person (frozen project band × admitted hours → `f_j`). Euros land in a **subpool** and are split by local `p_j`. Contributors do not invoice the parent pool for this work. [ADR 2026-09-09](../docs/decisions/2026-09-09_project-as-contractor.md), [2026-09-09 log](../docs/log/2026-09-09_hours-cap-and-project-contractor.md). Direction A (distribute parent `p` to people) is **not** the live model.

**Next pass:** option 2 (contingent invoiced fee, points as weights) with **reduced complexity**. Working cap sketch: [docs/log/2026-09-04_option-2-effort-cap.md](../docs/log/2026-09-04_option-2-effort-cap.md) (points mint `p`; `f_ij` clips invoices; `P_t` is still the GA pool; `p` now amortizes as that cap is consumed). Hours-only ledger input: [2026-09-09 log](../docs/log/2026-09-09_hours-cap-and-project-contractor.md). Sub-projects: nested mint budgets ([nested-mint-budgets.md](nested-mint-budgets.md)), two levels, linear `p_j` first, project-as-contractor. A 2026-09-07 sketch that mints `S = a · C`, splits `P_t` by share of `S`, and burns `S_i ← S_i − R_i` euros is **not** that pass: the burn is a 1 `S` = €1 par, and `S` stays non-transferable — [docs/log/2026-09-07_s-burn-euro-par.md](../docs/log/2026-09-07_s-burn-euro-par.md). Belgian tax and corporate analysis: [token-system.md](token-system.md). DVB questions **(a)–(p):** [dvb-questions.md](dvb-questions.md). Cap-opening discussion (lots, year-1 1×, path to 10×): [docs/log/2026-09-10_pt-distribution-and-cap-opening.md](../docs/log/2026-09-10_pt-distribution-and-cap-opening.md). Q-token supplier-network access (**open**, not live spec): [docs/log/2026-09-10_q-token-supplier-network.md](../docs/log/2026-09-10_q-token-supplier-network.md). Tokens instead of shares to skip the inbreng-revisor (**open**, not live spec): [docs/log/2026-09-10_tokens-not-shares-avoid-revisor.md](../docs/log/2026-09-10_tokens-not-shares-avoid-revisor.md) (including: 10× of contribution + VenB/30% WHT does not remove arm’s length; two instruments vs gated option-2 10×). Earlier contractor-credit proposal: [docs/decisions/2026-09-02_tax-aware-contribution-credits.md](../docs/decisions/2026-09-02_tax-aware-contribution-credits.md).

## Intended flow (working constraints, payout not decided)

1. Contributor is admitted as a **member** of the CV (governance). Labour is **not** assumed to be volunteer work for tax purposes.
2. Ledger records **contribution points**, then mints weights with `p = c0 · c^k` (early work mints more). No euro quote of `dc/dp`. Sub-projects may mint local `p_j` without moving global `c` until the parent spends a mint budget; that root `p` is credited to the **project entity**, which invoices `P_t` into a euro subpool ([nested-mint-budgets.md](nested-mint-budgets.md)).
3. Weights are **non-transferable**. No peer market. Only **root** `p` (held by people or by project entities) shares in `P_t`. Local `p_j` splits the subpool in euros, not parent `p`.
4. **Do not** pay via extra cheap shares whose count tracks points, **do not** mint labour-quota shares on a steep bonding curve (including when revenues mint on that curve), and **do not** burn `p` at a euro par. **Do** amortize `p` against remaining opened cap ([p-burn-remaining-cap.md](p-burn-remaining-cap.md)). Vintages (budget `P_t`, default-in, time-opened cap, leftover to reserves) are **parked**, not the live spec; if they return, the same fraction burns **per lot**.
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
