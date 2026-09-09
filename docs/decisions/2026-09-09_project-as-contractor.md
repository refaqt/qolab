# ADR — Sub-project as contractor (euros in a subpool)

- **Date:** 2026-09-09
- **Status:** Accepted (design) for the nested **cash path**. Tax characterisation remains a DVB hypothesis.
- **Amends:** [2026-09-08 nested mint budgets](2026-09-08_nested-mint-budgets.md) points 1, 4, and 6 (who holds root `p`, what `p_j` splits, where euros land). **Does not un-accept** the mint gate: unofficial work still does not move parent `c`; parent still spends `A_{t,j}` / `B_{t,j}`.
- **Does not accept** option 1 vs 2. **Does not unpark** vintage lots. **Does not revive** cheap-share, bonding-curve shares, or `c × €1`. **Does not** attribute product revenue (or sale proceeds) to projects.

## Context

The 2026-09-08 nested-mint note gated root `p` so unproven work cannot dilute the parent curve, then **split that root `p` among contributors** of project `j`. Those people would have invoiced global `P_t` themselves.

That cash path is the wrong model. It forces the parent, on every mint, to decide **which local tasks** are in the grant and to blend **contributor hourly rates** into a cap for the lump. Contributors of `j` would also sit in the parent pool next to core contractors.

The intended object is simpler: a sub-project is a **contractor** with one rate and one invoice cap, like a person. Minting root `p` to that entity **accepts a lump of work at the project rate**. Euros from `P_t` go to the project’s **subpool**. Local `p_j` only splits **euros** inside `j`.

[2026-09-08 Direction B](../log/2026-09-08_nested-p-sunset-two-directions.md) asked for this analysis and warned against `c × €1`. The cap object is documented effort: admitted hours × **frozen project band**.

Full note: [token-system-design/nested-mint-budgets.md](../../token-system-design/nested-mint-budgets.md). Session: [docs/log/2026-09-09_hours-cap-and-project-contractor.md](../log/2026-09-09_hours-cap-and-project-contractor.md).

## Decision

1. **Recipient of root `p` is the project entity**, not the contributors of `j`. People inside `j` do not hold parent `p` unless they also work on the parent as themselves.
2. **The project is handled like a person:** frozen project band, `f_j` (invoice ceiling), remaining opened cap, share of `P_t` by its root `p`, [amortize that `p` against remaining opened cap](2026-09-08_p-burn-remaining-cap.md).
3. **Minting root `p` to `j` accepts past (or ongoing) work at the project rate.** `Δf_j` = admitted hours × project band. Admitted hours come from the parent’s point budget (`A_{t,j}`), not from filtering local tasks or averaging contributor rates. Do not size `A_{t,j}` from a euro valuation of the project.
4. **Euros land in `j`’s subpool.** Contributors invoice that subpool, split by local `p_j`, clipped by their own `f`. They do **not** invoice `P_t` for this work. Local `p_j` is not a claim on `P_t`.
5. **`P_t` stays one solvency-checked pot**, split by root `p` (people and project entities). Complementary goods still share by the project being admitted to that weight club — not by attributing turnover to a product line.
6. **Direction A** (local pot of parent `p` distributed to people) is **not** the live model. Future nested analysis uses this ADR.

## Consequences

- Parent governance never accepts individual sub-project tasks and never computes a blended rate for a mint.
- Catch-up of undocumented backlog is an attested **hour inventory** on the local ledger, then a parent admit at the **project** rate. Unofficial calendar time does not open `f_j`.
- Stronger grant-time evidence at first `B_{t,j} > 0` (the entity is now a contractor on `P_t`); still not a published par if `A_{t,j}` is in points. Ask DVB **(o)** (project-entity invoice; subpool invoices).
- Option-2 machinery is copied once: the same split / clip / fractional burn, first at parent→project, then at project→people.
