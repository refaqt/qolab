# ADR — The option-2 cap is one row per contributor

- **Date:** 2026-09-14
- **Status:** Proposed (pending counsel and a DVB prefiling). Nothing is launched by this ADR.
- **Supersedes:** the per-lot cap of [ADR 2026-09-03 time-opened fee cap](2026-09-03_time-opened-fee-cap.md) **for the live option-2 path**. That ADR stays as the record for the [parked vintage packaging](../../token-system-design/parked/vintage-pools.md), where lots still make sense.
- **Amends:** the "do not publish `r`" constraint in the [path map](../../token-system-design/README.md), with one narrow carve-out for a contracted contributor's own statement.
- **Does not change:** the mint `p = c0 · c^k`, the pool `P_t`, default-in and forfeiture, the fractional burn of `p` ([ADR 2026-09-08](2026-09-08_p-burn-remaining-cap.md)), the nested mint budgets ([ADR 2026-09-08](2026-09-08_nested-mint-budgets.md)), or the project-as-contractor cash path ([ADR 2026-09-09](2026-09-09_project-as-contractor.md)).
- **Does not decide:** the values of `r` and `k`. It also does not revive [fallback B](../../token-system-design/paths/option-2-contingent-fee/README.md) or move the large multiple back onto the effort base ([ADR 2026-09-14 two bases](2026-09-14_two-bases-10x-off-effort.md) still holds).

## Context

The live option-2 cap tracked a **lot** for every accepted block of work. Each lot had its own documented effort, its own paid total, its own opened ceiling, its own freeze state, and a place in an oldest-first queue. A contributor could not answer a simple question — "what may I still invoice?" — without replaying all of that.

This is the same weight that already got the vintage packaging parked once ([ADR 2026-09-04](2026-09-04_cheap-share-route-dead-end.md)). That ADR also left the standing warning: a simpler story that fails characterisation is not an improvement on a correct but heavy design. So the goal here is a simpler cap that keeps every fact the tax argument rests on.

It is worth naming what was missing. Until now the repo measured "easy to explain" against the **tax administration** only. Nothing anywhere set out to make the cap easy for a **contributor**. That was a real gap, and it is what this change fixes.

The proposal that started this was a single running number:

```
cap(n+1) = cap(n) · (1 + r) + effort(n) − paid(n)      r = 0.25
```

The one-number goal is right and this ADR takes it. The arithmetic is not, for three reasons.

1. **No lid.** `(1 + r)^n` is unbounded: about 9× documented effort after ten unpaid years, about 87× after twenty, about 808× after thirty. Option 2 targets at or near 1× on the effort base. An unbounded ceiling also matches the "unbounded claim on all future surplus" pattern that points at a hidden dividend, which is the expensive failure, not the cheap one.
2. **No freeze.** Growth applies to the whole balance, including the part left over after the documented work has been fully paid. A contributor paid in full keeps a remainder that grows every year for ever on work that is no longer at risk: €10,000 paid in full leaves €2,500, then €3,125, then €3,906, and so on. That is the trailing coupon the repo already rejected, and it is the exact pattern that reads as interest on a repaid balance.
3. **It breaks the burn.** Weight retires by `p · alloc / rem`. If `rem` grows without bound, the fraction burned per euro falls towards zero, weight never retires, and the longest waiter ends up holding both the largest ceiling and the most durable weight in every later split. That is the seniority hole the burn exists to close.

## Decision

Until counsel and a DVB prefiling say otherwise:

1. **The option-2 cap is one row per contributor.** Lots are retired for this path. For contributor `i` in year `n`:

   ```
   U_i(n)   = max(0, E_i(n−1) − A_i(n))
   O_i(n)   = min( O_i(n−1) + r · U_i(n),  (k − 1) · E_i(n) )
   cap_i(n) = E_i(n) + O_i(n)
   rem_i(n) = max(0, cap_i(n) − A_i(n))
   ```

   `E_i` is cumulative documented effort, `A_i` is cumulative allocations (counted whether or not invoiced), `U_i` is documented effort that was already on the books at the start of the year and is still not covered at its end.

2. **Three of the old rules now follow from the formula instead of being stated separately.** Work accepted this year opens nothing until it has survived one full allocation round unpaid, because `U` is built from `E_i(n−1)`. The opening stops on its own when allocations reach documented effort, because the term is then zero, and the already-opened remainder stays invoiceable. The ceiling never passes `k` times documented effort, because of the lid.

3. **The opening is linear, not compound.** `r` multiplies unrecovered **effort**. It never multiplies a balance. This also settles the two different meanings of `r` that were both in the repo: the additive form in the [2026-09-04 log](../log/2026-09-04_option-2-effort-cap.md) wins, the multiplicative form in [ADR 2026-09-03](2026-09-03_time-opened-fee-cap.md) does not.

4. **`r` is explained as an opening factor on work still at risk, never as a rate on a balance.** The argument, in order: there is no principal, because work was supplied and not money; there is no claim, because the pool may be zero and the row may lapse; the opening stops when the work stops being at risk; and it is bounded. Full text in [spec §5.2](../../token-system-design/paths/option-2-contingent-fee/README.md) and [DVB item (h)](../../token-system-design/analysis/dvb-questions.md).

5. **The publication rule is split, not dropped.** Public and promotional material, and any framing as a return or a yield, stay banned. A **contracted contributor** may receive a statement of **their own** row: documented effort, unrecovered effort, current ceiling, allocations to date, and the number of past years in which the pool was zero. No forward projection, no euros per `p`, no annualised figure, and not the words *balance*, *saldo*, *tegoed*, *outstanding* or *owed*. Limits in [annex-terms.md](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md) clauses 24 to 27.

6. **The CV instructs its accountant in writing** that the ceiling is not a liability and not a receivable, and that no provision or financial charge is recognised as the opening accrues, and offers the contributor the same note for theirs.

## Consequences

- A contributor needs one row and one formula. Exit, death and exclusion also collapse from a per-lot table to three one-line effects.
- The oldest-unpaid-lot-first queue disappears, and with it an open question.
- Freeze and the lid stop being rules a reader has to remember, which is the point: the two facts the interest argument depends on are now impossible to drop by accident.
- **A parameter change now hits everyone in the same year.** There is no lot vintaging left to stagger it. A reduction still applies to future opening only.
- **A sunset `T` changes shape.** There is no lot to lapse, so a sunset stops the opening and leaves the remaining ceiling invoiceable. Still an open question.
- Reviving fallback B now costs two decisions, not one: the retired per-lot machinery and the larger `k`.
- The numbers move. At `r = 0.25`, a fully unpaid row reaches 1.25× after one year, 1.50× after two, 2.25× after five, and stops at the lid. Under the proposed compound form the same row would have reached about 9× after ten years and kept going.
- `k` is now the only thing standing between this design and an unbounded ceiling. It cannot stay an open question for ever.
