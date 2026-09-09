# 2026-09-08 — Nested `p` sunset: local p-pool vs project-as-contractor

**Role(s):** finance, business-dev

**Closed 2026-09-09:** Direction B is the live cash path, specified in [ADR 2026-09-09](../decisions/2026-09-09_project-as-contractor.md) and [nested-mint-budgets.md](../../token-system-design/nested-mint-budgets.md). The project cap is admitted hours × **project band**, not `c × €1`. Direction A (local pot of parent `p` distributed to people) is **not** the live model. Session: [2026-09-09 log](2026-09-09_hours-cap-and-project-contractor.md). The mint gate of [ADR 2026-09-08](../decisions/2026-09-08_nested-mint-budgets.md) is unchanged. This log stays as the fork record.

## What happened

Nested mint budgets are already the accepted **mint gate** ([nested-mint-budgets.md](../../token-system-design/nested-mint-budgets.md), [ADR 2026-09-08](../decisions/2026-09-08_nested-mint-budgets.md)): unofficial work does not move parent `c`; the parent later spends a mint budget; cash pool `P_t` stays global. Still open: how local weight `p_j` / `p_ij` **sunsets** when a sub-project distributes, and whether the sub-project’s own pool is parent `p` or euros.

Two directions. **Direction A** (local pot of parent `p`, personal `p_cap`, linear `c` so only `c` is needed) is the proposal under review; it still has loose ends. **Direction B** (the sub-project is a contractor on the parent, internal rules the same, income in euros) is probably more elegant and is the **next analysis**. Neither is accepted here. This does **not** un-accept nested mint budgets or the proportional burn of root `p` ([ADR 2026-09-08 p-burn](../decisions/2026-09-08_p-burn-remaining-cap.md)).

**Prevention rules applied:** [do not put a unit price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not treat remaining `p` as remaining euros](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not keep paid-off weight as seniority](../mistakes/2026-09-08_unburned-p-after-cap.md). `× €1` on dimensionless points is already called out in the [option-2 effort-cap sketch](2026-09-04_option-2-effort-cap.md).

---

## Direction A — local pot of parent `p`, personal `p_cap`

Same work, same contribution points, parent or sub-project. Sub-project mint also logs how much parent `p` that `Δc` would mint (`p_cap`). The local pot is **parent `p`**, not euros. Split this pool by local `p_ij / Σ_i p_ij` (one project at a time; **not** summed across projects). No opt-out: everyone who has not reached `p_cap` receives `p`. Cap opens with time from mint of local `p_ij`, not from when `p` arrives in the pot. Hard limit on opening: **5× or 10×**. After a receipt:

```
p_ij ← p_ij · (1 − (parent p received in this pool this period) / p_cap)
```

If everyone who still has rem has hit `p_cap` and parent `p` is left in the pot that year, leftover `p` is **burned** and the **parent curve goes back** (that mint is undone).

Working hypothesis for this direction: **drop the bonding curve; `p ∝ c` (linear), so the ledger only needs `c`.** Early-bird then lives in **cap opening** (unpaid wait toward 5×/10×), not in `Δp/Δc`. Linearity also removes Jensen / curve-reset: “would have been minted on the parent” is just `Δc`, independent of current parent `c`. A busy bad project still must not move parent `c` until the parent admits a mint (same gate as nested mint budgets).

Risky sub-projects: with `p_cap` taken from the parent-equivalent mint, you do **not** earn more parent `p` for the same `Δc` than you would on the main project. Extra return is only (i) sharing a pot that core-only work does not get, and (ii) a higher opened multiple if the wait is long. A local bonding curve *without* `p_cap` could have paid more parent `p` to first movers on a new `j`; that is what `p_cap` forbids.

### What was misread, and what still needs a formula spec

Local `p_ij` and `p_cap` do **not** need to be the same scale. The burn is a **dimensionless fraction**: numerator and denominator are both parent `p`. Local `p_ij` is only a split key. Minting new `p_ij` does not, by itself, break that identity.

What still breaks a **blended** personal stock: new work added while old rem is already opening. Last week’s `Δc` inherits years of waited multiple — the lot problem ([gold rush](../mistakes/2026-09-03_immediate-multiple-gold-rush.md)). Independent of the curve and of scale.

The written burn also needs **which** `p_cap` sits in the denominator:

| If you mean | Apply to | After two fills of 50 from `p_cap = 100` |
| --- | --- | --- |
| Lifetime `p_cap`, this period’s receipt, current `p_ij` | `50 · (1 − 50/100) = 25` left at rem 0 | leftover local weight ([unburned `p`](../mistakes/2026-09-08_unburned-p-after-cap.md)) |
| **Remaining** opened cap before this allocation | `50 · (1 − 50/50) = 0` | correct |
| Lifetime `p_cap`, **cumulative** receipt, **original** `p_ij` | closed form `p_0 · (1 − cum / p_cap)` | correct if no new mint on the stock |

The accepted parent identity is the middle row: `p ← p · (rem − alloc) / rem`; `rem = 0` ⇒ `p = 0`. Haircut on the allocated slice. Direction A should write that, not leave `p_cap` ambiguous.

No opt-out plus leftover-to-burn (parent `c` reversed) is the analogue of default-in plus leftover of `P_t` to reserves: the pot is a **flow**, not a growing stock. That answers the idle-pool objection **if** leftover never sits for next year. Forced receipt of `p` (not euros) is still a grant-time tax question (DVB, below).

### Why opening a **`p`-cap** is not the same object as opening the parent fee cap

On the parent, `r` and `k` do not grow `p`. They grow an **invoice ceiling on documented effort** `f` / `E_L` (hours × frozen contractor band). `p` is only the split key; it then burns as the **fraction** of that remaining **euro** rem just allocated. Same work, same euro cap, different `Δp` if the mint were curved — which is why `(k × E) / Δp` is not a unit price of `p` ([ADR 2026-09-04](../decisions/2026-09-04_fee-cap-not-unit-price.md)).

A time-opened **`p_cap`** grows a ceiling **in parent `p`**. One logged unit can become 5 or 10 units of extraction rights if unpaid. That is a multiple **on the token stock** (or on points, if linear), not on quoted euro effort.

Consequences:

1. **Bands drop out of this layer.** Uniform points per hour → same `c` → same `p_cap` for a junior hour and a senior hour. Parent rem still distinguishes them via `f`. Nested `p_cap` does not, unless `f` still clips something later (there is no euro invoice at this layer).
2. **`k×` cannot be filled from this work’s own mint.** If the pot is the parent `p` minted for this `Δc`, the pot is about `1×` logged `p_cap`. Opening to 5×/10× only binds if **more** parent `p` later flows into the same pot (stream of mint budgets, later grants). That can be intended (risk premium if the project later receives a fat `p` flow). It is a different story from “this lot’s unpaid euro effort opens toward `k × E_L`.”
3. **Remaining `p_cap` reads as remaining tokens.** Parent remaining rem is “you cannot invoice more than this many euros of contingent fee.” Remaining `p_cap` is “you may still take this many `p`.” Stronger grant-time evidence; do not dashboard it as owed. Freeze after 1× **paid**, or a forecasted fat pot plus 5–10× already opening is the [gold rush](../mistakes/2026-09-03_immediate-multiple-gold-rush.md) again.
4. **Reversing parent `c` when leftover `p` burns** is well-defined if mint is linear (`c ← c − leftover`). On a bonding curve, “the curve goes back” depends on *which* `c` you unwind. Another reason A wants linear.

Complexity: nested copies of the same mechanism are acceptable **if** they really are the same. A `p`-denominated rem vs a euro `f` rem is **not** the same mechanism until that is written down.

### Loose ends still on A (why it is not the next pass)

- Specify rem vs lifetime `p_cap` in the burn; `p := 0` at rem 0.
- Lots vs blended `p_ij` when people add work while rem > 0.
- Freeze after 1× paid vs 5–10× opening as a trailing coupon.
- Where extra `p` in the local pot comes from if opened caps exceed this work’s mint; leftover burn + reverse `c` vs a later stream.
- Grant-time tax of forced `p` receipt; DVB on remaining `p_cap` as consideration.
- Whether linear `c` replaces the parent bonding curve globally or only inside nesting.
- Two clocks (local `p_cap` from mint vs parent euro rem from first root-`p` eligibility) — [nested mint](../../token-system-design/nested-mint-budgets.md) already starts the fee-cap clock at first root `p`, not at unofficial accept.

---

## Direction B — sub-project as contractor (next analysis)

The sub-project runs **internally like the parent** (points, split, opened cap, proportional burn). Its income is **euros**. It gets that income because the parent mints `p` **for the project entity** (when admitted — parent `c` does not move on unofficial local logging) and the project then receives euros from the parent’s distribution (`P_t · p_j / Σ p`, clipped by the project’s rem). People inside `j` never hold parent `p` unless they also work on the parent as themselves.

That keeps the dilution gate: a very active **unadmitted** project cannot mess up parent `c` or `P_t`. It is the nested-mint idea with the **recipient of parent `p` / parent euros** being the project, not the contributors.

Working constraint from this pass: the project’s cap must **not** be “the value of all the work they did” in a way that lets `j` extract far more than comparable parent-side work. Proposed ceiling to analyse: **`c` points × €1**.

That `× €1` on points collides with existing hygiene ([option-2 sketch](2026-09-04_option-2-effort-cap.md): `× €1` on dimensionless `c` is a published par; [ADR 2026-09-04](../decisions/2026-09-04_fee-cap-not-unit-price.md); [cheap-share euro par](../mistakes/2026-09-04_cheap-share-euro-par.md)). The analysis has to pick a cap object that still stops over-extraction without writing 1 point = €1: likely the same documented-effort `f` as a person, applied to the project as one contractor (sum of internal `f`, or a parent-chosen admitted budget), **not** `c × €1` unless counsel says otherwise.

Direction B also **conflicts on purpose** with nested mint budgets’ “do not split euros by project” (complementary goods, silos, forks). That is why it needs a detailed pass, not a quiet swap.

---

## Not taken (this pass)

| Sketch | Why not now |
| --- | --- |
| All work (core and sub-project) mints parent `p` to the **person** and advances parent `c` | A very active bad project would move the parent curve and the global split. |
| Escrow a **real** parent mint at local accept | Same: parent `c` moves when local work is logged. |
| Local split linear in `c_ij` with **no** local early-bird object | Removes the incentive to start a risky local project (no intra-project founding weight, no extra pot logic). |

---

## Decisions

Proposed (not accepted):

1. Keep **both** directions on the record. Direction A is the local `p`-pot / `p_cap` sketch, with linear `c` so only `c` is needed and early-bird in cap opening (5×/10× hard limit). Direction B is project-as-contractor with euro income.
2. Direction A has **too many loose ends** (burn denominator, lots, freeze vs 5–10×, leftover reverse-`c`, tax of forced `p`, `p`-rem vs `f`-rem). Do not implement it next.
3. **Next step is Direction B** (more elegant on paper; still needs detailed analysis, including the project cap and the clash with “cash stays global”).
4. Do not un-accept nested mint budgets or root-`p` burn until B is written. Do not accept `c × €1` as a unit par in this log.

## Open Questions

- Direction B: project rem = internal `Σ f`, parent-admitted euro budget, or `c × €1`? How to stop over-extraction without a points-as-euros par.
- Direction B vs complementary products: can a tool that only ships with the machines still be paid if euros stop at project `j`?
- Parent mint to the **project entity**: linear `p_j ∝ c_j` vs parent bonding curve; who holds `p_j` after the project invoices (burn against the project’s rem).
- Double layer: project burns parent `p` as it takes euros; people inside burn local weight as they take project euros.
- Whether linear `c` should replace the parent bonding curve even if B wins (early-bird only in cap opening).
- DVB: forced receipt of `p` (A); project as the invoicing contractor (B); remaining `p_cap` vs remaining `f`.

## Next Steps

- Write the Direction B analysis (project-as-contractor, same internal mechanism, euro income, dilution gate preserved). Resolve the project cap without `c × €1` unless that collision is accepted on purpose.
- After that, either amend nested mint budgets or reject B and return to A with the loose ends closed.
- Counsel + accountant stay on (a)–(d), (h)–(j), and nested (k)–(n); add the project-entity invoice if B is pursued.
