# 2026-09-09 — Hours-only ledgers, freeze remainder, project as contractor

**Role(s):** finance, business-dev

## What happened

Worked through how to set contribution points `c` and the invoice ceiling `f` without publishing a price of `c` (and then of weights `p`). Also corrected the nested-project cash path: the 2026-09-08 mint gate still stands, but **sub-projects receive euros**, not a lump of root `p` to split among people.

### Two ledgers, one input (hours)

A task board (roles, small tasks, projects) is UX. The ledger has two columns with different jobs:

| Ledger | What | Job |
| --- | --- | --- |
| Contribution points `c` | Same score for the same work (uniform **100 points per hour** for everyone) | Mint weights `p` |
| Documented effort `f` | Hours × **frozen contractor band**, or a quoted effort in the annex | Invoice **ceiling** at cash-out |

Uniform 100 points/hour only **renames hours**. It must not be chosen because the job is €100/hour. Industry rates stay **off** the points rule. Do **not** mint `p` from `f` (that reconstructs `w = df/dp` in €/`p`). Do not publish `(k × f) / Δp` or `remaining / p`. `× €1` on dimensionless points is a published par.

**One degree of freedom per accepted item: hours.** Then `c = hours × 100` and `f = hours × frozen band`. Roles (hours/week), small tasks (hour estimate), and projects (larger hour estimate) are the same two columns. Hours per week on a role is a commitment; log `c` and `f` when the work is **accepted**. Work in year `Y` first sits in `P_{Y+1}`.

A band is frozen at join / task accept (or, for a sub-project entity, at contractor join). It is not a live “my market rate.” Contract wording: `f` is quoted effort / reference fee for a **ceiling**. There is no hourly invoice. Compensation is a contingent success fee **if** a pool exists. Do not write “fees he would normally have invoiced.” Do not dashboard remaining cap as “€X still owed.”

**Do not derive points from euros.** That *is* an exchange rate. Safe: hours → both `c` and `f`. Unsafe: pick euros and points together; `c = f / (euros per point)`; `hours = euro_budget / band` then `c = 100 × hours` (band on the points path); size a mint from a euro valuation of a project.

Actual pay is still `min(share of P_t, remaining opened cap)`. `hours × rate` is the ceiling, not the invoice.

### Freeze after 1× paid

Freeze means **stop raising the ceiling**. It does **not** mean “you may only ever collect 1×” and it does **not** forfeit headroom already opened. After a long unpaid wait that opened the cap to 3×, a round that pays 1× leaves **2× still invoiceable**; `p` burns by `alloc / rem` (one-third), so two-thirds of that lot’s weight remains. If that round’s pool is large enough, the invoice is `min(gross, remaining opened cap)` — they take the opened 3×, not a forced 1×.

If the cap is already at lifetime `k×`, freeze and “keep opening” are the same for later drought years: nothing opens past `k`. The extra multiple compensates **unpaid principal** (`paid < f`), not calendar time after the work has been paid at 1×. Opening after `paid ≥ f` is the rejected trailing coupon / gold rush (“age-opens-cap even after repayment”) and looks like interest on a balance (DVB **(h)**). Illiquidity of unpaid **upside** is a different risk; the remaining opened headroom *is* the premium from the first wait. Optional later knob (not accepted): a tight extra bound on unpaid remainder only, lots kept separate. Do not raise `k` or drop freeze to “make the second wait fair.”

Keep **lots**, not one blended personal cap (new hours must not inherit old waited multiple).

### Sub-projects: euros in, `p_j` only inside

Wrong model (do not use in further analysis): parent mints root `p`, the sub-project **splits that `p` among contributors**, and those people invoice `P_t` themselves.

**Live model:** the sub-project is handled **like a person** — frozen **project rate**, documented effort `f_j`, invoice cap, root `p` held by the **project entity**. The project invoices `P_t` (clipped by the project’s rem). **Euros** land in the project’s **subpool**. Inside, euros are split using local `p_j`. Contributors do **not** take money from the parent pool.

Providing the sub-project with root `p` **is accepting past work, at the project rate.** Parent does not filter which local tasks are in the grant and does not compute an averaged hourly rate from contributors. Admitted hours (from the mint budget in points) × project band → `Δf_j`. Otherwise every mint would need a task-level accept list and a blended rate.

Work yet to do: task description → hours; same hours × 100 for local `c_j` and hours × project rate for the entity’s `f` once the parent admits. Work already done: log hours onto the local ledger **when accepted** (including a one-time attested inventory for undocumented backlog). Do not reconstruct 2021 invoices in year 3. Unofficial years do not open the **euro** cap; that clock starts at first root-`p` eligibility for the project. Parent still gates how many points are admitted (`A_{t,j}`); inflating local `c_j` does not enlarge the pie.

This is Direction B from [2026-09-08 nested `p` sunset](2026-09-08_nested-p-sunset-two-directions.md), specified so that the project cap is **hours × project band**, not `c × €1`. Direction A (local pot of parent `p` split to people) is not the live model.

Wrote [ADR 2026-09-09](../decisions/2026-09-09_project-as-contractor.md). Amended [nested-mint-budgets.md](../../token-system-design/nested-mint-budgets.md).

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not treat remaining `p` as remaining euros](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not keep paid-off `p` as seniority](../mistakes/2026-09-08_unburned-p-after-cap.md).

## Decisions

Proposed (hours / freeze / task board; not a new ADR): two ledgers; hours-only input; 100 points/hour as a weight scale; freeze = stop opening, remainder stays payable; projects are big tasks in hours.

Accepted (design, cash path): [ADR 2026-09-09](../decisions/2026-09-09_project-as-contractor.md) — project entity holds root `p` and invoices like a person at the **project rate**; euros to a subpool; internal split by `p_j`. Does not un-accept the 2026-09-08 mint gate. Does not accept option 1 vs 2. Does not unpark vintages. Does not accept `c × €1`. Does not attribute product revenue to projects.

## Open Questions

- Internal fee-cap clock for contributors invoicing the subpool (first subpool eligibility vs local accept).
- Whether unrecognized local `c_j` is retired on each parent admit without slicing `p_j` by task (working default: yes — retire admitted points so they are not uploaded twice; `p_j` burns only as people take subpool euros).
- Complementary products: a tool that only ships with the machines still shares via the **project’s** root `p` in global `P_t`; confirm that is enough so people do not also need parent `p`.
- Tight extra illiquidity bound on unpaid remainder after 1× (not accepted).
- DVB **(o)**: project entity as invoicing contractor; contributors invoice the subpool.

## Next Steps

- Counsel + accountant on (a)–(d), (h)–(j), nested (k)–(n), and **(o)**.
- Keep option-2 spec on hours-only ledgers and project-as-contractor; do not analyse further as if people received root `p` from `j`.
