# Proportional burn of `p` against remaining opened cap

**Status: accepted (design).** Tax characterisation is still a DVB hypothesis, not a ruling. Companion to the option-2 effort-cap sketch ([docs/log/2026-09-04_option-2-effort-cap.md](../docs/log/2026-09-04_option-2-effort-cap.md)) and the parked vintage note ([vintage-pools.md](vintage-pools.md)). ADR: [2026-09-08](../docs/decisions/2026-09-08_p-burn-remaining-cap.md).

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not treat remaining `p` as remaining euros](../docs/mistakes/2026-09-04_cheap-share-euro-par.md); [do not open a lifetime multiple on day one](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not keep paid-off `p` as seniority on later work](../docs/mistakes/2026-09-08_unburned-p-after-cap.md).

This is **not** the rejected burns: not `cash / w`, not `v = pool / N`, not 1 `p` = €1, not `S ← S − €`.

---

## Direct answers

| Question | Working answer |
| --- | --- |
| After all caps are paid, then everyone contributes again at the **same** point on the bonding curve: do veterans take more of every later vintage? | **Yes, if paid-off `p` is still there.** The curve is global, so the same new `Δc` mints the same `Δp`. The extra return is leftover historical weight, not extra risk on this work. |
| Can we burn `p_i · (revenue_i / remaining_cap_i)`? | **Yes.** `remaining_cap_i` is remaining **opened** cap **before** this vintage’s allocation. Filling the cap burns all `p`. Receiving nothing burns nothing. |
| Is that a euro par on `p`? | **No.** It retires a **fraction** of personal (or per-lot) weight. Implied €/`p` is `rem_i / p_i`, which differs by person and mint date. Do not publish that quotient. What stays rejected is a **unit FX**: the same euros per token for everyone (`w`, `v = P/N`, 1 `p` = €1, `S − €`). |
| Does taking a vintage still leave the right to the next one? | **Partially.** You keep participating until remaining opened cap is 0, but weight falls in proportion to cap consumed. That is the point: paid work should not keep a full claim on later flows. |

---

## The hole without a burn

The option-2 sketch splits `P_t` by stock of `p` and only **clips** with remaining effort cap. It did not burn `p`.

The mint `p = c0 · c^k` is a **global** curve on cumulative points. Anyone contributing **now** is at the same `c`. Equal new work mints equal `Δp` and (if freeze-after-1×) opens equal new remaining cap. Early-bird is “this `Δc` vs an earlier `Δc`”, not “veteran vs newcomer this year”.

If a veteran’s cap is already filled and their old `p` is still outstanding, a new contribution is added **onto** that stock:

| | Veteran | Newcomer |
| --- | --- | --- |
| New work | same `Δc`, same `Δp`, same new rem | same |
| Weight in the split | old `p` + `Δp` | `Δp` only |
| This vintage | fills the new cap almost immediately | drips |

Same risk on the new work; very different share of every later `P_t`. That is seniority from **already-paid** weight.

Parked vintages already **retired a lot** when its opened cap was exhausted. The simpler per-person sketch dropped that retirement. This note puts a continuous version back.

---

## Accepted rule

Let `rem_i` be remaining **opened** fee cap of contributor `i` **before** this vintage’s allocation (`opened cap − already paid`; freeze-after-1× still binds). Let `gross_i = P_t · p_i / Σ p`. Let

```
alloc_i = min(gross_i, max(0, rem_i))
```

`alloc_i` is what this vintage assigns, whether or not they invoice. Cash `R_i` (invoice) equals `alloc_i` on default-in. Uninvoiced / opt-out slices still **forfeit to operating reserves** and still haircut `p` (otherwise sitting out preserves weight for a fatter year).

Then:

```
if rem_i <= 0:
    p_i ← 0
else:
    burned_i = p_i · (alloc_i / rem_i)
    p_i      ← p_i − burned_i
             = p_i · (rem_i − alloc_i) / rem_i
```

Invariant on a payout: **`p / rem` is unchanged** (until rem hits 0, when `p` is zeroed). You retire the same fraction of weight that you just took of cap.

When they invoice, `alloc_i = R_i`, so this is the proposed identity

```
burned_i = p_i · (revenue received by i in this vintage) / (remaining cap of i)
```

### Guards (part of the feature)

1. **Denominator is remaining opened cap before pay**, not lifetime `k × effort`. Dividing by `k×` while the opened cap is `1×` would burn only `1/k` of `p`; after freeze, leftover `p` would sit with `rem = 0` and the hole returns. When opened rem hits 0, **`p := 0`** even if lifetime `k×` was never reached. Do not evaluate `alloc / rem` at `rem = 0`.
2. **Apply every vintage from the start.** Equal treatment of new work needs `p = 0` **before** the new mint, not a one-shot reset mixed with new rem. Mixing old `p` with new rem lets the veteran vacuum until that new rem is filled.
3. **Haircut on `alloc_i`**, not only on cash received. Default-in; leftover of `P_t` to **reserves**, not an earmarked `p` pot. Opt-out must not preserve `p`.
4. **Do not publish `rem_i / p_i`** or dashboard “€X of cap still represented by `p`.” Do not book remaining cap or remaining `p` as a receivable.
5. **Per-lot if lots exist.** Same fraction on lot `L`: `p_L · alloc_L / rem_L`. A blended per-person `p` / `rem` lets a new lot inherit old waiting ([gold rush](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md)). The option-2 personal cap may keep one `p_i` and one `rem_i`; then continuous application (guard 2) is what fixes the “caps filled, then everyone contributes again” case. If they add work while `rem_i > 0`, new `Δp` and new rem stack on the same stock — lots are the fix if that inheritance shows up.

Opening rem with `r` while unpaid: `p` stays, `rem` grows, so `p / rem` falls; a later payout then burns fewer tokens per euro. At exhaustion, remaining `p` still goes to 0. Do not describe `r` as interest.

---

## Worked numbers

Curve is global. Both contribute **now**: `Δc` mints `Δp = 50`, new documented effort opens `rem = €5,000`. `P_t = €20,000`. Only these two people.

### Without burn (paid-off `p` still there)

Veteran still holds 10,000 `p` from work whose cap is already paid. After the new mint: veteran 10,050 `p`, newcomer 50 `p`. `Σp = 10,100`.

| | Gross | Invoice (clipped) |
| --- | ---: | ---: |
| Veteran | €19,901 | **€5,000** |
| Newcomer | €99 | **€99** |

Same new risk; veteran takes the new cap in one vintage. Newcomer drips. If they both keep contributing, this repeats.

### With the burn, applied from the start

When the veteran’s old cap filled, `rem = 0` ⇒ `p = 0`. After the new mint both have 50 `p` and `rem = €5,000`. `Σp = 100`.

| | Gross | Invoice | Burned `p` | `p` after |
| --- | ---: | ---: | ---: | ---: |
| Veteran | €10,000 | €5,000 | 50 | 0 |
| Newcomer | €10,000 | €5,000 | 50 | 0 |

Equal new work, equal split, both caps filled, both weights retired. Next contribution again starts from `Δp` only.

### Partial vintage (`P_t = €1,000`), same 50 / 50 start

`alloc = €500` each. `burned = 50 · 500 / 5000 = 5`. Each keeps 45 `p` and €4,500 rem. Ratio `p / rem` unchanged. Next vintage they still split equally.

A uniform euro burn (`S ← S − €`) would have haircut both by the same factor **and** written 1 `S` = €1. This fraction does not.

---

## Why this is not a unit price of `p`

| Construction | Used here? |
| --- | --- |
| `w = dc/dp` in €/`p` | No |
| `v = P / N` (spot on a growing stock) | No |
| 1 `p` = €1 or `S_i ← S_i − R_i` euros | No |
| Invoice clip `pay ≤ rem` on documented effort | Yes (already in the option-2 cap) |
| Retire the **fraction** `alloc / rem` of that person’s (or lot’s) `p` | Yes |

The payout is still a budget split clipped by an effort ceiling. Burn does not convert tokens into euros; it amortizes **weight** as that ceiling is consumed. `rem_i / p_i` is not unique to `p` (same work, different mint dates, different `Δp`). A real unit FX is the same for all outstanding tokens at a date.

Operationally, remaining `p` **is** linear in remaining opened cap for that person or lot. That is more grant-time evidence than “weights never burn.” It is still not a published par. Do not make it one. DVB item **(j)** below.

Wait-and-run against `v = P/N` stays dead: leftover of `P_t` goes to reserves; missing a year does not fatten tomorrow’s pot. The new game (skip a thin year to keep `p`) is closed by default-in plus haircut on `alloc_i`.

---

## What this does not accept

- Option 1 vs option 2 (still pick the tax box separately).
- Unparking vintage lots (still parked for complexity). If they return, use the same fraction **per lot**.
- Day-one lifetime `k×`, a published €/`p`, or remaining `p` as remaining euros.
- Transferable `p`.

---

## DVB / counsel

Existing items **(a)–(d)** and **(i)** (effort cap vs implied €/`p`) still apply. Add:

- **(j)** Proportional burn of `p` against remaining opened cap: is remaining `p` remaining consideration, or still a dimensionless weight plus an invoice ceiling?

Full catalog: [dvb-questions.md](dvb-questions.md).

Until that sign-off, do not describe the burn as “€X per certificate” or “paying `p` down in euros.”
