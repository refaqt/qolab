# ADR — Nested mint budgets for sub-projects

- **Date:** 2026-09-08
- **Status:** Accepted (design) for sub-projects. Tax characterisation remains a DVB hypothesis.
- **Does not accept** option 1 vs 2; that remains the next pass for cash-out.
- **Does not unpark** vintage lots. **Does not revive** cheap-share or bonding-curve shares. **Does not** split euros by project.
- **Amends:** mint / ledger comments in [2026-09-02](2026-09-02_tax-aware-contribution-credits.md) (still proposed). Compatible with [2026-09-08 proportional burn of `p`](2026-09-08_p-burn-remaining-cap.md) on **root** `p` after it is granted.

## Context

Work that is off-roadmap, risky, or not yet believed should not mint **root** `p` (global weights that share in `P_t`). If it never mints, a later success has no fair split of who did the unpaid years. Splitting **euros** by project fails when a sub-project only sells with other products (no honest attribution), pushes people to silo, and cannot reward a dependency or fork that lifts Refaqt as a whole.

The cooperative thesis stays: a small piece of work shares in **global** success. Nesting is for **governance** (sub-projects accept their own contributions) and **mint allocation** (parent gates how much new root `p` a project may receive), so bad or unproven projects cannot dilute good projects’ `p`.

A one-shot grant of `p` sized like a purchase is a buyout. The need is a **funding stream**: the parent may admit root `p` more than once.

Full note: [token-system-design/nested-mint-budgets.md](../../token-system-design/nested-mint-budgets.md).

## Decision

1. **Accept** nested mint budgets as the sub-project route. Cash pool `P_t` stays global, split only by root `p`.
2. **Local ledger:** project `j` accepts work, logs `c_j`, `f`, and mints **`p_j`**. Default local mint is linear. `p_j` is not a claim on `P_t`. Global `c` / `p` do not move until the parent spends budget.
3. **Parent sets the pie.** Each period, `B_{t,j}` (default: admitted points `A_{t,j}`) is chosen by the parent, **not** computed from reported `c_j`. Failed / unproven: `B_{t,j} = 0`. Inflating `p_j` cannot tax other projects.
4. **Stream, not buyout.** Repeat `B_{t,j}` while the project stays on the mint list. Do not size a grant from a euro valuation of the project. Catch-up grants split by stock of `p_j` and retire recognized local weight; ongoing grants follow new local work. Same local work is not minted into root `p` twice.
5. **Late on the global curve is intended.** Intra-project early-bird lives in `p_j`. Unofficial years do not get cheap global `Δp`.
6. **Fee cap** for that work opens from **first root-`p` eligibility**, not from unofficial accept. Root `p` then amortizes against remaining opened cap ([2026-09-08](2026-09-08_p-burn-remaining-cap.md)).
7. **Contracts exist during unofficial work** (dienstenovereenkomst + IP/CLA + contingent QOLAB annex). Two levels to start. Ask DVB **(k)–(n)** on the nested-mint note.

## Consequences

- Complementary tools and forks share via global `P_t` once admitted; no project euro waterfall.
- Unproven work cannot dilute root `p`. Proven-late work enters as a stream of weights, not a sale of the project for `p`.
- Top-level governance does not accept sub-project contributions; it only allocates mint budget and `P_t`.
- Stronger grant-time evidence at first `B_{t,j} > 0` than ordinary mint; still not a published par if budgets are in points / `Δp`, not euros.
- Option-2 complexity stays on one euro pool plus a mint list. Local bonding curves are optional and discouraged for small teams.
