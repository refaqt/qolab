# Nested mint budgets for sub-projects

**Status: accepted (design) for sub-projects.** Tax characterisation is still a DVB hypothesis, not a ruling. Mint gate: [ADR 2026-09-08](../docs/decisions/2026-09-08_nested-mint-budgets.md). Cash path: [ADR 2026-09-09](../docs/decisions/2026-09-09_project-as-contractor.md) — the **project entity** holds root `p` and invoices `P_t`; **euros** land in a subpool and are split internally by `p_j`. Does **not** accept option 1 vs 2. Does **not** unpark vintages. Does **not** attribute product revenue to projects. Does **not** mint root `p` to contributors of `j`.

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not dress labour-quota cheap shares as a dividend](../docs/mistakes/2026-09-04_cheap-share-euro-par.md); [do not keep paid-off `p` as seniority on later work](../docs/mistakes/2026-09-08_unburned-p-after-cap.md); [steep curve vs usable later mint](../docs/mistakes/2026-09-07_steep-curve-low-grant.md).

Nesting is **who may mint root `p`** (dilution gate) plus **who invoices `P_t`** (the project as a contractor). It is not a product-revenue waterfall. Do not analyse this as “parent `p` is distributed to people inside `j`.”

---

## Direct answers

| Question | Working answer |
| --- | --- |
| Who receives root `p` for work on `j`? | The **project entity**. Contributors of `j` do not hold parent `p` unless they also work on the parent as themselves. |
| Who receives euros? | The project invoices `P_t` into a **subpool**. Local `p_j` splits **those euros**. Contributors do not invoice the parent pool for this work. |
| How is the project’s invoice cap set? | Like a person: frozen **project band** × admitted hours → `f_j`. Minting root `p` to `j` **accepts that lump of work at the project rate**. Parent does not filter local tasks or average contributor rates. |
| A tool only ships with the machines; how much revenue is “the software”? | **Do not attribute turnover to a product line.** One pool `P_t`, split by **root** `p` (people and project entities). Complementary work shares because the project is admitted to that weight club. |
| Off-roadmap work the community will not mint `p` for — then it succeeds years later. How is it rewarded? | Local ledger (`c_j`, `p_j`) while unproven. Parent later starts a **stream** of mint budgets. The **project** receives root `p` (and `Δf_j` at the project rate). Euros later sit in the subpool; historical `p_j` splits them. |
| If the sub-project never makes it, does global `p` move? | **No.** `B_{t,j} = 0`. Local `p_j` never becomes a claim on `P_t`. Other projects are not diluted. |
| Is this “Refaqt buys the project for an amount of `p`”? | **No.** Recurring mint budget, not a one-shot `Δp` sized like a purchase price. Never back `B_{t,j}` out of a euro valuation of the project. |
| Who accepts individual contributions? | The **sub-project**. The parent only chooses which projects are on the mint list and the **size** of `B_{t,j}` / `A_{t,j}`. |
| Does `p_j` participate in vintages / `P_t`? | **No.** Only root `p` does. `p_j` is a split key for the **subpool in euros**. |
| Why not project success fees from attributed sales? | Attribution is impossible for complementary goods; silos follow; a fork of project 1 that lifts Refaqt would not reward project 1. Global `P_t` plus gated mint of root `p` **to the project** does. |

---

## Wrong model (do not use)

Parent mints root `p` → sub-project **splits `p` among people** → those people invoice `P_t`.

That path is what [ADR 2026-09-09](../docs/decisions/2026-09-09_project-as-contractor.md) replaces. It would require, on every mint, a filter of which local tasks are accepted and an averaged hourly rate for the lump. Direction A on [2026-09-08 nested `p` sunset](../docs/log/2026-09-08_nested-p-sunset-two-directions.md) (a local pot of parent `p`) is **not** the live spec.

---

## Two layers

### Project `j` (including unproven / unofficial)

- Maintainers accept work. Parent does not review each contribution.
- Ledger input is **hours** (roles, small tasks, and the project itself are the same columns). `c_j = hours × 100` (uniform; industry rates stay off the points rule). Mint local weights **`p_j`**. Default: **linear** `p_j ∝ c_j`. A local bonding curve is optional and easy to give first movers almost all `p_j`.
- Log personal documented effort `f` when the work is accepted (ceiling on **subpool** invoices later). Contract + IP/CLA + QOLAB annex **during** this work: compensation is a contingent success fee **if** the project later invoices a pool. Do not reconstruct hours in year 3; an undocumented backlog may be accepted once as an attested hour inventory.
- `p_j` is **non-transferable**. No euro quote of `dc_j / dp_j`. **`p_j` cannot invoice `P_t`.**
- The **project entity** has its own frozen **project band**. That band is not a blend of contributor rates.
- Global `c` and global `p` do **not** move until the parent admits work.

### Refaqt (parent)

- Root `p` is minted only when the parent spends a **mint budget** `B_{t,j}` on project `j`.
- Unproven / failed: `B_{t,j} = 0`.
- If `B_{t,j} > 0`, mint that period’s root `p` on the **global** curve at today’s `c` and **credit it to the project entity**. That mint **accepts** a lump of local work **at the project rate**:

```
A_{t,j}     ≤  unrecognized local c_j     # cannot upload more than exists
hours_j     =  A_{t,j} / 100              # uniform points per hour
f_j        ←  f_j + hours_j × project_band
c          ←  c + A_{t,j}
Δp          =  p(c_new) − p(c_old)        # global p = c0 · c^k, held by j
unrecognized local c_j  ←  unrecognized local c_j − A_{t,j}
```

- The project then invoices like any contractor: `pay_j = min(P_t · p_j_root / Σ p, remaining opened cap on f_j)`. **Euros go to `j`’s subpool.** Root `p` amortizes against that rem ([p-burn-remaining-cap.md](p-burn-remaining-cap.md)).
- Inside `j`, the subpool is split by local `p_j`; personal `f` clips; local `p_j` amortizes as people take euros. Same mechanism, one layer down.
- Inflating local `c_j` / `p_j` does not enlarge `A_{t,j}`; it only fights over a parent-sized pie (and over the internal split).

Do **not** allocate `B_{t,j}` by converting a euro value of the project into `p`. Direct `Δp` as the budget is an open alternative (easier to explain, easier to abuse as a certificate printer). Do **not** set `f_j = c × €1`.

---

## Stream, not buyout

| | Buyout | Mint stream (accepted) |
| --- | --- | --- |
| How often | One `Δp` | Repeat `B_{t,j}` while the project stays on the mint list |
| Size | Looks like a price | Governance line: “this much effort is admitted this period” at the **project rate** |
| Same local work twice | N/A | **No.** Retire recognized local **points** (`c_j`) so they cannot be uploaded again |
| Euro valuation → `p` | Forbidden | Forbidden |
| Who gets the `Δp` | — | The **project entity** |

A spin-out / IP sale in euros is a different box (not this route). This route is nested **admission to the weight club**, with the club member being the project.

### Catch-up vs ongoing

1. **Catch-up** (wilderness already done): parent marks grants as recognition of backlog. The project receives root `p` and `Δf_j` at the **project rate** (no task filter, no averaged contributor rate). Retire the admitted slice of unrecognized `c_j` so that labour is not minted into root `p` again. Do **not** slice local `p_j` by which tasks were in the grant — `p_j` stays the internal euro split key and burns when people take subpool euros.
2. **Ongoing:** new local work mints new `p_j` and adds unrecognized `c_j`. Later `B_{t,j}` can admit more. The project can receive root `p` many times without a purchase.

Do not leave paid-off **root** `p` on the project as seniority after its rem is 0 — same hole as [unburned root `p` after the cap](../docs/mistakes/2026-09-08_unburned-p-after-cap.md). Same for local `p_j` after a person has exhausted their subpool rem.

### Late on the global curve

Unofficial years do **not** get cheap global `Δp`. Intra-project early-bird lives in `p_j`. Versus the rest of Refaqt, admitted work sits at **today’s** `c`. That is the price of the dilution gate: optionality without taxing other projects until the parent admits the work.

---

## What the parent decides vs the sub-project

| Parent (Refaqt) | Sub-project `j` |
| --- | --- |
| Mint list and `A_{t,j}` / `B_{t,j}` each period | Which contributions are accepted onto `c_j`, `p_j`, personal `f` |
| Global euro budget `P_t` (one pot, solvency-checked) | Project band; `f_j` from admitted hours × that band |
| Pays the **project entity** (invoice clipped by `f_j`) | Splits **euros** in the subpool by `p_j` |
| Does **not** accept individual sub-project contributions | Does **not** mint root `p`; does **not** invoice `P_t` as a person for this work |

Unused `B_{t,j}` should **expire** with the period (a flow), not roll into a hoard of unminted certificates. Exact expiry vs roll is still open; expiry is the default.

Two levels are enough to start. Deeper nesting is the same protocol (a project is parent to its sub-projects: child invoices the parent’s subpool, not grandparent `P_t`). Recursion is how governance scales; it is also how the system becomes unexplainable — do not require it in the option-2 pass.

---

## Fee cap and tax hygiene

- Open `r` / `k×` on **`f_j`** from **first root-`p` eligibility** for the project, not from year 1 of unofficial logging. A sale year plus years of “unpaid opening” on wilderness hours recreates the [day-one lifetime multiple](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md).
- Freeze after 1× of `f_j` is paid **stops further opening**; it does not forfeit remaining opened headroom ([2026-09-09 log](../docs/log/2026-09-09_hours-cap-and-project-contractor.md)).
- Do not book remaining mint budget, remaining `p_j`, remaining root `p`, or remaining cap as a receivable.
- Do not publish `€/p`, `€/p_j`, or `rem / p`.
- Recognition (first `B_{t,j} > 0`) is a more sensitive grant-time moment than ordinary mint — still a hope until `P_t` exists, but tied to “we now believe this project.” DVB **(k)–(o)** below.
- Employees stay on euro payroll. Nested `p_j` is not a third labour status.

---

## What this does not accept

- Attributing `P_t` (or sale proceeds) by product line as the catch-up mechanism.
- Minting root `p` to **people** for sub-project work, or splitting parent `p` inside `j`.
- Parking unofficial `c_j` on the **global** curve “in escrow” (that would move everyone else’s mint as soon as local work is logged).
- A one-shot `Δp` calibrated to a euro purchase price.
- `f_j = c × €1`, or any unit par on `p` / `p_j`.
- Bonding-curve **shares**, cheap-share quotas.
- Filtering local tasks / averaging contributor rates in order to set the project cap.
- Option 1 vs 2 (still pick the tax box separately).
- Unparking vintage lots (still parked for complexity).

---

## Open choices (parameters, not the route)

- Parent allocates **`A_{t,j}` in points** (default; `Δp` and `Δf_j` fall out) vs allocates **`Δp` directly**.
- Who sets `B_{t,j}`: GA, a mint committee, a published cap per project per year. Must not be “€X of value ÷ a price of `p`.”
- Internal fee-cap clock for people invoicing the subpool (first subpool eligibility vs local accept). Working default: do not open personal rem on unofficial calendar time.
- Unused budget expires vs rolls (default: expire).
- Depth of nesting beyond two levels.
- Whether a local bonding curve is ever worth it inside a small team.

---

## DVB / counsel

Existing items **(a)–(d)**, **(i)** (effort cap vs implied `€/p`), and **(j)** (proportional root-`p` burn) still apply. Nested **(k)–(o)** below. Full catalog: [dvb-questions.md](dvb-questions.md).

- **(k)** Delayed mint of root `p` after unofficial logged work: taxable event at local accept, at first `B_{t,j} > 0`, or still only at invoice?
- **(l)** `p_j` as a non-claim on `P_t`; only a split key for the subpool.
- **(m)** Parent-chosen mint budgets vs implied value of the project (especially at a commercialisation vote).
- **(n)** Fee-cap clock on `f_j` starting at first root `p`, not at local accept.
- **(o)** Project entity as invoicing contractor; contributors invoice the subpool, not `P_t`.

Until those sign-offs, do not describe `p_j` as “already worth a share of Refaqt” or size `B_{t,j}` in euros.
