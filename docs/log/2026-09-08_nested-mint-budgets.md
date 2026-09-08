# 2026-09-08 — Nested mint budgets for sub-projects

**Role(s):** finance, business-dev

## What happened

Needed a way to reward off-roadmap work that did not receive root `p`, without splitting euros by project (a complementary tool that only ships with the products has no honest revenue split) and without letting unproven work dilute global `p`. Project-only success fees would silo people and would not reward a dependency or fork that lifts Refaqt.

Accepted route: **cash stays global**; nesting is a **gated stream of root `p`**. Sub-projects mint `p_j` (split key only). Parent chooses mint budget `B_{t,j}` independently of reported `c_j`. Failed projects send 0; global `p` unchanged. Catch-up splits by stock of `p_j`; ongoing grants can repeat (funding stream, not a buyout). Wrote [token-system-design/nested-mint-budgets.md](../../token-system-design/nested-mint-budgets.md) and [ADR 2026-09-08](../decisions/2026-09-08_nested-mint-budgets.md).

## Decisions

Accepted (design) for sub-projects: nested mint budgets as above. Does not accept option 1 vs 2. Does not unpark vintages. Does not split `P_t` by project. Does not size `B_{t,j}` from a euro valuation. Fee-cap clock from first root `p`. Root `p` still amortizes against remaining opened cap. DVB **(k)–(n)** added.

## Open Questions

- Allocate admitted points `A_{t,j}` vs direct `Δp`.
- Who sets `B_{t,j}` (GA / committee / policy cap).
- How to retire recognized `p_j` on catch-up (pro-rata vs oldest lots).
- Unused budget expires vs rolls (default: expire).
- Nesting deeper than two levels.

## Next Steps

- Keep this mint route in the option-2 spec (two levels, linear `p_j` first).
- Open fork on how local weight sunsets / whether the sub-project takes euros: [nested `p` sunset two directions](2026-09-08_nested-p-sunset-two-directions.md) (next analysis: project-as-contractor).
- Counsel + accountant on (a)–(d), (i), (j), and (k)–(n).
