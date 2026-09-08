# Nested mint budgets for sub-projects

**Status: accepted (design) for sub-projects.** Tax characterisation is still a DVB hypothesis, not a ruling. Does **not** accept option 1 vs 2. Does **not** unpark vintages. Does **not** split euros by project. ADR: [2026-09-08](../docs/decisions/2026-09-08_nested-mint-budgets.md).

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not dress labour-quota cheap shares as a dividend](../docs/mistakes/2026-09-04_cheap-share-euro-par.md); [do not keep paid-off `p` as seniority on later work](../docs/mistakes/2026-09-08_unburned-p-after-cap.md); [steep curve vs usable later mint](../docs/mistakes/2026-09-07_steep-curve-low-grant.md).

Cash stays **global**. Nesting is **who may mint root `p`**, not a revenue waterfall.

---

## Direct answers

| Question | Working answer |
| --- | --- |
| A tool only ships with the machines; how much revenue is “the software”? | **Do not split euros by project.** One pool `P_t`, split by **root** `p`. Complementary work shares by being admitted to that weight club. |
| Off-roadmap work the community will not mint `p` for — then it succeeds years later. How is it rewarded? | Local ledger (`c_j`, `p_j`) while unproven. Parent later starts a **stream** of mint budgets. Historical `p_j` splits those grants. Holders then have root `p` and sit in global `P_t` like everyone else. |
| If the sub-project never makes it, does global `p` move? | **No.** `B_{t,j} = 0`. `p_j` never becomes a claim on `P_t`. Other projects are not diluted. |
| Is this “Refaqt buys the project for an amount of `p`”? | **No.** Recurring mint budget, not a one-shot `Δp` sized like a purchase price. Never back `B_{t,j}` out of a euro valuation of the project. |
| Who accepts individual contributions? | The **sub-project**. The parent only chooses which projects are on the mint list and the **size** of `B_{t,j}`. |
| Does `p_j` participate in vintages / `P_t`? | **No.** Only root `p` does. `p_j` is a split key for incoming root `p`. |
| Why not project success fees? | Attribution is impossible for complementary goods; silos follow; a fork of project 1 that lifts Refaqt would not reward project 1. Global `P_t` plus gated mint of `p` does. |

---

## Two layers

### Project `j` (including unproven / unofficial)

- Maintainers accept work. Parent does not review each contribution.
- Log contribution points `c_j` and mint local weights **`p_j`**. Default: **linear** `p_j ∝ c_j` (uniform points per hour; industry rates stay off the points rule). A local `p = c0_j · c_j^{k_j}` is optional and easy to give first movers almost all `p_j`.
- Log documented effort `f` when the work is accepted (invoice ceiling later). Contract + IP/CLA + QOLAB annex **during** this work: compensation is a contingent success fee **if** root `p` is later granted and a pool exists. Do not reconstruct hours in year 3.
- `p_j` is **non-transferable**. No euro quote of `dc_j / dp_j`. **`p_j` cannot invoice `P_t`.**
- Global `c` and global `p` do **not** move.

### Refaqt (parent)

- Root `p` is minted only when the parent spends a **mint budget** `B_{t,j}` on project `j`.
- Unproven / failed: `B_{t,j} = 0`.
- If `B_{t,j} > 0`, mint that period’s root `p` on the **global** curve at today’s `c`, give the lump to project `j`, which splits it by `p_j`.
- Those people now hold root `p` and share in **all** future `P_t` (machines, tools, forks). That is the coop deal.
- Root `p` then follows the already-accepted payout rules: option-2 invoices from `P_t`, effort cap, [amortize `p` against remaining opened cap](p-burn-remaining-cap.md).

Default size of the grant: parent chooses **admitted points** `A_{t,j}` (a cap, not “whatever `c_j` you reported”). Then

```
A_{t,j}  ≤  unrecognized local c_j     (cannot upload more than exists)
c        ←  c + A_{t,j}
Δp       =  p(c_new) − p(c_old)        # global p = c0 · c^k
```

`Δp` is split among holders of `p_j`. Inflating local `c_j` / `p_j` does not enlarge `A_{t,j}`; it only fights over a parent-sized pie.

Do **not** allocate `B_{t,j}` by converting a euro value of the project into `p`. Direct `Δp` as the budget is an open alternative (easier to explain, easier to abuse as a certificate printer).

---

## Stream, not buyout

| | Buyout | Mint stream (accepted) |
| --- | --- | --- |
| How often | One `Δp` | Repeat `B_{t,j}` while the project stays on the mint list |
| Size | Looks like a price | Governance line: “this much effort is admitted this period” |
| Same local work twice | N/A | **No.** Retire recognized local weight (below) |
| Euro valuation → `p` | Forbidden | Forbidden |

A spin-out / IP sale in euros is a different box (not this route). This route is nested **admission to the weight club**.

### Catch-up vs ongoing (two jobs, both in `p`)

1. **Catch-up** (wilderness already done): parent marks grants as recognition of backlog. Split `Δp` by **stock** of `p_j`. Retire the recognized slice of `p_j` (and the matching unrecognized `c_j`) so that work is not minted into root `p` again.
2. **Ongoing:** new local work mints new `p_j`. Later `B_{t,j}` splits that. The project can receive `p` many times without a purchase.

Do not leave paid-off local weight as seniority on later `B_{t,j}` for **new** work — same hole as [unburned root `p` after the cap](../docs/mistakes/2026-09-08_unburned-p-after-cap.md). Catch-up installments may pay the same backlog over several periods; that is retiring the backlog, not a permanent coupon on `p_j`.

### Late on the global curve

Unofficial years do **not** get cheap global `Δp`. Intra-project early-bird lives in `p_j`. Versus the rest of Refaqt, admitted work sits at **today’s** `c`. That is the price of the dilution gate: optionality without taxing other projects until the parent admits the work.

---

## What the parent decides vs the sub-project

| Parent (Refaqt) | Sub-project `j` |
| --- | --- |
| Mint list and `A_{t,j}` / `B_{t,j}` each period | Which contributions are accepted onto `c_j`, `p_j`, `f` |
| Global euro budget `P_t` (still one pot, solvency-checked) | Split of incoming root `p` by `p_j` |
| Does **not** accept individual sub-project contributions | Does **not** mint root `p` |

Unused `B_{t,j}` should **expire** with the period (a flow), not roll into a hoard of unminted certificates. Exact expiry vs roll is still open; expiry is the default.

Two levels are enough to start. Deeper nesting is the same protocol (a project is parent to its sub-projects). Recursion is how governance scales; it is also how the system becomes unexplainable — do not require it in the option-2 pass.

---

## Fee cap and tax hygiene

- Open `r` / `k×` from **first root-`p` eligibility** for that work, not from year 1 of unofficial logging. A sale year plus years of “unpaid opening” on wilderness `f` recreates the [day-one lifetime multiple](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md).
- Do not book remaining mint budget, remaining `p_j`, or remaining cap as a receivable.
- Do not publish `€/p`, `€/p_j`, or `rem / p`.
- Recognition (first `B_{t,j} > 0`) is a more sensitive grant-time moment than ordinary mint — still a hope until `P_t` exists, but tied to “we now believe this project.” DVB **(k)–(n)** below.
- Employees stay on euro payroll. Nested `p_j` is not a third labour status.

---

## What this does not accept

- Splitting `P_t` (or sale proceeds) by project as the catch-up mechanism.
- Parking unofficial `c_j` on the **global** curve “in escrow” (that would move everyone else’s mint as soon as local work is logged).
- A one-shot `Δp` calibrated to a euro purchase price.
- Bonding-curve **shares**, cheap-share quotas, or a euro par on `p` / `p_j`.
- Option 1 vs 2 (still pick the tax box separately).
- Unparking vintage lots (still parked for complexity).

---

## Open choices (parameters, not the route)

- Parent allocates **`A_{t,j}` in points** (default; `Δp` falls out of the global curve) vs allocates **`Δp` directly**.
- Who sets `B_{t,j}`: GA, a mint committee, a published cap per project per year. Must not be “€X of value ÷ a price of `p`.”
- How to retire recognized `p_j` on catch-up (pro-rata vs oldest local lots). If parked lots return, prefer per-lot.
- Mix of catch-up vs ongoing in the same period.
- Unused budget expires vs rolls (default: expire).
- Depth of nesting beyond two levels.
- Whether a local bonding curve is ever worth it inside a small team.

---

## DVB / counsel

Existing items **(a)–(d)**, **(i)** (effort cap vs implied `€/p`), and **(j)** (proportional root-`p` burn) still apply. Add:

- **(k)** Delayed mint of root `p` after unofficial logged work: taxable event at local accept, at first `B_{t,j} > 0`, or still only at invoice?
- **(l)** `p_j` as a non-claim until the parent spends mint budget.
- **(m)** Parent-chosen mint budgets vs implied value of the project (especially at a commercialisation vote).
- **(n)** Fee-cap clock starting at first root `p`, not at local accept.

Until those sign-offs, do not describe `p_j` as “already worth a share of Refaqt” or size `B_{t,j}` in euros.
