# ADR — Hardware for experiments is funded by the ordinary bond, then lent by the company

- **Date:** 2026-09-14
- **Status:** Proposed (pending counsel). Nothing is launched or offered by this ADR.
- **Amends:** [option-2 §1 and §11](../../token-system-design/paths/option-2-contingent-fee/README.md) (documented effort stays hours and quoted work; hardware is not on that row); [capped-participating-bond §8](../../token-system-design/paths/capped-participating-bond/README.md) (a named use of the investor leg).
- **Supersedes:** nothing.
- **Does not change:** the mint, the option-2 cap, the bond row, the split `θ`, the freeze on the contributor leg, or the no-freeze rule on the investor leg.
- **Does not decide:** the Dutch wording of a loan-for-use contract; whether a modest hire is safer than a free loan; VAT on the purchase or on the loan; whether consumable materials use this path or ordinary project cost.
- **Does not revive:** [cheap shares](2026-09-04_cheap-share-route-dead-end.md), [*inbreng in nijverheid*](2026-09-10_inbreng-in-nijverheid-dead-end.md), or a large multiple on the effort base ([ADR 2026-09-14 two bases](2026-09-14_two-bases-10x-off-effort.md)).
- **Does not add a second instrument.** The bond is the one already proposed in [ADR 2026-09-14 investor leg](2026-09-14_investor-leg-capped-participating-bond.md). The equipment loan is an operational contract, not a token.

## Context

A contributor who wants to run an experiment may need hardware or equipment. Two naive answers fail the design.

1. **Put the cost on the effort row.** Documented effort is hours times a frozen band, or a quoted effort. Adding a machine's invoice would put euros of capital onto the labour ceiling. That rebuilds a euro price next to hours, which is the comparable the option-2 defence is designed not to have ([2026-09-14 mistake](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md); [ADR 2026-09-14 two bases](2026-09-14_two-bases-10x-off-effort.md)).
2. **Let the contributor buy the machine and own it.** Then the tool sits outside the company. That fights the mission: Refaqt exists in part to democratize access to manufacturing tools ([mission.md](../mission.md)). It also leaves the company with no asset if the person leaves.

The investor leg already takes **cash** and gives a **subordinated, contingent** claim. That is the right box for "I put money in so this experiment can have a tool."

## Decision

Until counsel says otherwise:

1. **Hardware for an accepted experiment is company property, funded as capital, not as labour.** It does not enter `f`, `E`, `c`, or `p`. It is not reimbursed from `P^C_t`.

2. **The sequence is three steps, and they stay three contracts.**
   1. The contributor who wants the experiment **subscribes to the ordinary capped participating bond**, in cash, on the same terms as any other holder ([path note](../../token-system-design/paths/capped-participating-bond/README.md)).
   2. The CV **buys the equipment** from its treasury (which now includes that cash) and **takes title**.
   3. The CV **lends the equipment** to the contributor for the experiment (a loan for use; Dutch wording is counsel's: *bruikleen*, not the bond).

3. **There is no hardware-bond class and no earmark in the instrument.** The only things that vary per holder remain the amount and the year. The offering document does not tie a position to a serial number, a project, or a person's hours. The board may still decide, operationally, to buy a named tool after a subscription. That decision lives in the purchase file and the loan-for-use contract, not in the Loan Regulations.

4. **The contributor holds a bond, not the machine.** If the CV fails, they have a subordinated claim like any other holder. They cannot take the tool in lieu of repayment. Exclusion as a bad-leaver contributor does not touch the bond ([loan-regulations clause 21](../../token-system-design/paths/capped-participating-bond/loan-regulations.md)); the company may still recall the tool because it owns it.

5. **Cash in is real, and it is not a function of the labour ledgers.** The amount advanced is the cash the person chooses to subscribe. It is not a formula of hours, `c`, `p`, or the contributor row ([path note §8](../../token-system-design/paths/capped-participating-bond/README.md)). Netting an unpaid fee into a subscription is still forbidden.

6. **The three documents never mix.** The contributor annex does not describe the bond or the tool. The offering document does not describe the contributor ceiling, `r`, `k`, or the experiment. The loan-for-use contract does not describe either token instrument.

## Pair check

Facts the contributor leg needs to stay **absent**, and whether this use supplies them:

| Absent fact | Does this use supply it? |
| --- | --- |
| No principal on the labour row | No. Principal stays on the bond, which already exists. |
| No euro price per hour | **Risk.** Sizing the subscription from hours, or writing "€X of tools for Y hours," publishes a rate. Forbidden. The amount is chosen cash. |
| No unit conversion of `p` | No. The tool is not minted, burned, or priced in `p`. |
| Ceiling never booked as a liability | No. The bond principal is already a liability; the machine is an asset. The labour ceiling stays off the books. |
| `r` never published as a return | No. The offering document still states only `r_I` and `k_I`. |

A second implied conversion to watch: euros of tools next to a person's hours. Do not compute it. Do not put it in any compelled disclosure.

## Consequences

- The company owns the tool. That matches the mission (shared access to manufacturing equipment) and keeps the asset if the person leaves.
- The person who funded it is an ordinary holder. They take the same contingent repayment as any investor. They do not get a private machine plus a bond.
- Ordinary company capex without a matching subscription stays allowed. This ADR is the path when a contributor wants to put money in so the experiment can have a tool.
- Durable equipment is in scope. Consumable materials (items used up in a run) are **not** decided here.
- Counsel items: benefit in kind if the tool is used privately; VAT on the purchase and on a loan for use; whether a modest hire is safer than a free loan; what happens if the tool is destroyed.
