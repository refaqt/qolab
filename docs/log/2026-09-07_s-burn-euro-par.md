# 2026-09-07 — Burn of S at euro par (option-2 sketch)

**Role(s):** finance, business-dev

## What happened

Investigated a simpler option-2 sketch:

- Contributor is a CV **member** (governance share) and an entity that can **invoice** (no employees; labour is not volunteer work).
- Contribution points `dC` mint weights `dS = a · dC`; `S_i ← S_i + dS`.
- Each year the GA sets a pool `P_t`. Contributor `i` invoices `R_i = P_t · S_i / Σ S`.
- Burn: `S_i ← S_i − R_i` (euros subtracted from `S`).
- Yearly mint decay: `a ← a · (1 − r)`, so later work mints less `S` per point.

Three questions.

### Does the burn put a price on `S`?

**Yes. It puts a par of 1 `S` = €1.** Uncertainty of this year’s `P_t` does not undo that.

Pro-rata of an unknown pool (`R_i = P_t · S_i / Σ S`) is only this vintage’s budget split. That residue, by itself, is what vintages already accepted. Subtracting **euros** from `S` is a **unit FX** (a conversion rate, like a foreign-exchange rate: each euro invoiced retires one `S`). Remaining `S` is remaining euros if later pools cover the stock. Same class of fact as burning 5,000 `p` per €5,000 ([cheap-share euro par](../mistakes/2026-09-04_cheap-share-euro-par.md)) and as remaining `p` = remaining euros ([ADR 2026-09-04](../decisions/2026-09-04_fee-cap-not-unit-price.md)).

`dS = a · dC` then makes `a` a €/point mint. If year-1 `a = 1`, grant is “1 point → €1 of remaining claim.” If `P_t > Σ S`, `S_i − R_i` goes negative unless clipped; clipping makes the par louder (euro cap, open on day one → gold rush at about `a ×` points-as-euros).

What would **not** price `S`: keep it as a dimensionless weight; split `P_t` by share of `S`; do **not** burn `S` for taking the vintage. Retire via a documented-effort ceiling, sunset, or exit. An effort cap on the **invoice** is not a unit FX of `S` (it does not convert tokens into euros).

### Can `S` be transferable?

**No, if the goal is a contingent service fee with no grant-time price.**

A peer market (even among member BVs) prints a euro price; FPS can copy it onto later mints. Option 2 needs the contractor who did the work to invoice; a transferee invoices for work they did not do (assignment / investment, not a dienstenovereenkomst). Off-chain issuer-only is how the draft stays outside MiCA; a euro-par unit plus peer transfer is also e-money-shaped. With 1 `S` ≈ €1 face, the secondary quote confirms the par and concentrates claims.

Residual that is not a market: transfer only back to the issuer (exit / forfeiture); universal succession on BV merger.

### Other problems

- **Burn does not reallocate among incumbents.** `S_i′ = S_i · (1 − P_t / Σ S)` haircuts every participant by the same factor. Relative shares among existing holders are unchanged. The burn only shrinks the stock (new `dS` is less diluted) and writes a euro par. It does not implement “you got paid, so you have less claim than someone who waited.”
- **Opt-out restores wait-and-run.** If `S` burns only when cash is taken, holders skip the invoice until a fat year. Leftover of `P_t` must go to **operating reserves**, not an `S`-earmarked pot; uninvoiced weight must forfeit for that vintage ([idle pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md)).
- **Day-one multiple.** With burn-at-par, `a` is a lifetime euro ceiling per point. Calendar `a` is not the parked “open at 1× documented effort, raise only while unpaid” rule ([gold rush](../mistakes/2026-09-03_immediate-multiple-gold-rush.md)).
- **Calendar decay of `a` is a cliff.** Everyone minting in the same year gets the same `a`. Work piles into December of a high-`a` year. This `r` is mint decay, not the vintage cap-opening `r`.
- **One ledger.** The working option-2 sketch keeps points → weights separate from documented effort `f` → invoice ceiling. Here `S` is both. Same-year work in the same `P_t` looks like this year’s wage (record date: work in `Y` first sits in `P_{Y+1}`).
- **If the system is meant to pay `S` down, `S` is a delayed euro debt.** Intended 1:1 burn makes every minted unit eventually €1, merely timed by the GA.
- **`P_t` must be a fee budget**, not “profit the GA sets aside,” or the invoice story and a dividend story land on the same instrument. Solvency cap: `min(policy % of profit or EBITDA, cash after reserves)`, not an automatic 10% of turnover.
- **“No private persons” is stricter than “must invoice.”** A zelfstandige / eenmanszaak can invoice. Forcing a BV selects for people who already have a company. Refaqt employees stay on euro payroll.
- **GA conflict:** contributors are members who vote on `P_t`; statutory waterfall has to bind.

Worth keeping: membership for admission, invoicing through a taxable entity, a GA/board `P_t`, default-in split of **this year only**, early-bird in the **mint** (not in a rising `€/S` rate). Drop `S_i ← S_i − R_i`.

## Decisions

Proposed (not accepted): this sketch is **not** the next option-2 pass as written. Keep the skeleton (member + invoice, `P_t`, default-in, mint-time early-bird). **Do not** burn weights against euros. **Do not** make `S` transferable among contributors. Same prevention rules as [cheap-share euro par](../mistakes/2026-09-04_cheap-share-euro-par.md); not a new incident. Bindings unchanged: [no unit `v`](../decisions/2026-09-03_vintage-pools-no-unit-price.md), [effort cap is not €/`p`](../decisions/2026-09-04_fee-cap-not-unit-price.md), [no day-one lifetime multiple](../mistakes/2026-09-03_immediate-multiple-gold-rush.md).

## Open Questions

- How little option-2 machinery is enough without a euro par: weights + `P_t` + a 1× (or documented-effort) cap, without lots that open over time? (Still open from [cheap-share log](2026-09-04_cheap-share-route.md).)
- Whether a uniform yearly `a` decay is simpler than `p = c0 · c^k` without introducing a December cliff.
- Who may invoice: BV only, or also eenmanszaak / foreign contractors.

## Next Steps

- Iterate option 2 with reduced complexity: no `S − €` burn, no peer transfer of weights.
- Counsel + accountant still required before anyone is promised a credit (DVB (a)–(d), (h), (i)).
