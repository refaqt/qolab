# ADR — Proportional burn of `p` against remaining opened cap

- **Date:** 2026-09-08
- **Status:** Accepted (design). Tax characterisation remains a DVB hypothesis.
- **Amends:** [2026-09-03 vintage pools](2026-09-03_vintage-pools-no-unit-price.md) point 4 (no burn for taking a vintage); the “No burn of `p`” line in the [2026-09-04 option-2 effort-cap sketch](../log/2026-09-04_option-2-effort-cap.md). Does not unpark vintage lots. Does not accept option 1 vs 2.
- **Does not revive** euro-par burns: [cheap-share](2026-09-04_cheap-share-route-dead-end.md), [`S ← S − €`](../log/2026-09-07_s-burn-euro-par.md).

## Context

The option-2 sketch splits each year’s budget `P_t` by share of `p` and clips invoices with remaining documented-effort cap. It did not burn `p`. After caps are filled, leftover historical `p` still sits in the split. The bonding curve `p = c0 · c^k` is **global**, so a veteran and a newcomer contributing **now** mint the same `Δp` for the same `Δc` and take the same risk on that work. The veteran nonetheless takes much more of every later vintage, because old weight is still there.

Parked vintages retired a lot when its opened cap was exhausted (a cliff). Euro-par burns (`cash / w`, `v = pool / N`, 1 `p` = €1, `S_i ← S_i − R_i`) are rejected: they put a unit conversion rate on the mint.

Proposed identity: burn `p_i · (revenue_i / remaining_cap_i)`.

Full note: [token-system-design/p-burn-remaining-cap.md](../../token-system-design/p-burn-remaining-cap.md).

## Decision

1. **Accept** amortizing `p` against remaining **opened** fee cap. Before this vintage’s allocation, `rem_i` is opened cap minus already paid. `alloc_i = min(P_t · p_i / Σ p, max(0, rem_i))`. Then `burned_i = p_i · (alloc_i / rem_i)` when `rem_i > 0`. When they invoice, `alloc_i` is revenue received, which is the proposed formula.
2. **When `rem_i = 0`, set `p_i := 0`.** Do not divide by zero. Do not leave paid-off weight outstanding. Do not use lifetime `k × effort` as the denominator while the opened cap is smaller.
3. **Apply every vintage from the start**, so new work after a filled cap mints onto `p = 0`.
4. **Haircut on `alloc_i`**, including forfeited / uninvoiced slices. Default-in; leftover of `P_t` to operating reserves. Opt-out must not preserve `p`.
5. **Do not publish** `rem_i / p_i` or treat remaining `p` as remaining euros. The burn is a **fraction of personal (or per-lot) weight**, not a unit FX. Still rejected: `w`, `v = P/N`, 1 `p` = €1, `S − €`.
6. If parked **lots** return, apply the same fraction **per lot**. A per-person blend may keep one `p_i` / `rem_i` for the simpler option-2 pass; then decision 3 is what fixes “everyone contributes again after all caps are filled.”
7. Ask DVB item **(j):** proportional burn vs remaining `p` as remaining consideration.

## Consequences

- Veterans and newcomers at the same point on the curve take the same share of later vintages for the same new work, once old caps have zeroed `p`.
- Taking a vintage no longer leaves **full** weight for the next one; it leaves the unpaid fraction of cap. That is intended.
- Wait-and-run against a rising `v` stays dead (flow + reserves). Skip-a-thin-year to keep `p` is closed by default-in plus haircut on `alloc_i`.
- Stronger grant-time evidence than never burning `p`; still not a published par if the quotient is not stored or communicated.
- Vintage packaging stays parked for complexity. Option 1 vs 2 is unchanged.
