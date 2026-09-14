# 2026-09-14 — The option-2 cap becomes one row; `r` explained as an opening factor

**Role(s):** finance, business-dev

**Prevention rules applied:** [no euro spot price on `p`](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [no day-one lifetime multiple](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [retire paid-off `p`](../mistakes/2026-09-08_unburned-p-after-cap.md); [art. 53, 10° for the excess test](../mistakes/2026-09-14_wrong-article-for-excess-test.md); [no multiple on the effort base](../mistakes/2026-09-14_10x-on-the-effort-base.md). One new rule comes out of this session: [no cap as a balance times `(1 + r)`](../mistakes/2026-09-14_cap-as-balance-times-one-plus-r.md). No text published here frames `r` as a return, and the only new disclosure is the contributor's own row.

## What happened

The question was how to simplify the cap. The complaint is fair: with lots, a contributor has to hold their effort, what was paid, how far the ceiling has opened, how much it opens next, and where each lot sits in a queue. Nobody can plan around that.

The proposal was one running number, `cap(n+1) = cap(n) · (1 + r) + effort(n) − paid(n)` with `r = 0.25`.

### Issues found with that form

1. **It is unbounded.** About 9 times documented effort after ten unpaid years, about 87 after twenty, about 808 after thirty. Option 2 aims at or near 1 times documented effort ([ADR 2026-09-14 two bases](../decisions/2026-09-14_two-bases-10x-off-effort.md)). An unbounded ceiling also matches the "unbounded claim on all future surplus" pattern that points at a hidden dividend, which is the expensive failure mode, not the cheap one.
2. **It deletes freeze.** Growth hits the whole balance, including what is left after the work has been paid in full. €10,000 paid in full leaves €2,500, then €3,125, then €3,906, for ever, on no new work. This is the trailing coupon, and per [DVB item (h)](../../token-system-design/analysis/dvb-questions.md) it is the exact shape that reads as interest on a repaid balance.
3. **It breaks the burn.** Weight retires by `p · alloc / rem`. With `rem` growing without a bound the burned fraction per euro falls towards zero. Weight never retires and the longest waiter holds both the biggest ceiling and the most durable weight. That is the hole the burn was written to close, reopened from the other side.
4. **Blending is one-way.** With one number you cannot tell which work a payment repaid. That is the mechanical reason a per-lot freeze is impossible under a blended cap, so freeze has to be rebuilt from something else or it is simply gone.
5. **A parameter change hits everyone at once.** No lot vintaging means a vote on `r` or `k` moves every contributor's ceiling in the same year.
6. **A sunset has nothing to lapse.** With no lots, `T` has to stop the opening instead.
7. **The letters collide.** The proposal used `f` for fees paid. In this repo `f` already means documented effort. Keeping those letters would have quietly inverted `f` across every earlier note.
8. **"Fees paid" is the wrong input.** Allocation is default-in. If the input is cash received, opting out both preserves and grows the ceiling.

### What was kept

The one-number goal, and the reason for it. Until now the repo measured "easy to explain" against the tax administration only. Nothing set out to make the cap easy for a **contributor**. That gap was real.

Two things also get simpler and stay simpler: exit, death and exclusion collapse to three one-line effects, and the oldest-unpaid-lot-first queue disappears along with its open question.

### The form adopted

```
U_i(n)   = max(0, E_i(n−1) − A_i(n))
O_i(n)   = min( O_i(n−1) + r · U_i(n),  (k − 1) · E_i(n) )
cap_i(n) = E_i(n) + O_i(n)
rem_i(n) = max(0, cap_i(n) − A_i(n))
```

The opening multiplies unrecovered **effort**, not a balance. Three old rules now fall out of the formula: new work opens nothing until it has survived one full allocation round unpaid; the opening stops on its own once allocations reach documented effort, with the opened remainder still invoiceable; and the ceiling never passes `k` times documented effort.

Checked by running the recursion at `r = 0.25`, `k = 3`:

| Vintage | 1 | 2 | 3 | 5 | 9 | 10+ |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| `cap / E`, never paid | 1.00 | 1.25 | 1.50 | 2.00 | 3.00 | 3.00 (lid) |

Paid in full in vintage 2: the opening term is zero from then on and nothing moves again. Paid €2,000 a year from vintage 2: the opening slows as the unrecovered part shrinks, stops in vintage 6, and the remaining ceiling drains to zero. Weight reaches zero when the ceiling is exhausted, and total allocations stop at exactly 3 times documented effort.

The change from compounding to linear is deliberate and it moves the numbers:

| Unpaid years | 1 | 2 | 5 | 10 | 20 | 30 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| `(1 + r)^n` | 1.25 | 1.56 | 3.05 | 9.31 | 86.74 | 807.79 |
| `1 + n · r` | 1.25 | 1.50 | 2.25 | 3.50 | 6.00 | 8.50 |

This also settles the two different meanings of `r` that were both in the repo. The additive form in the [2026-09-04 log](2026-09-04_option-2-effort-cap.md) wins; the multiplicative form in [ADR 2026-09-03](../decisions/2026-09-03_time-opened-fee-cap.md) does not.

### Why `r` is not an interest rate

Four facts, in the order to use them. There is **no principal**: interest is the price of using a sum of money that was lent or left available, and here work was supplied, not money. There is **no claim**: the pool may be zero in any year and the row may lapse unpaid, so a ceiling is not consideration "to be received" (WBTW art. 26). It **stops when the risk stops**: interest on a debt runs until the debt is repaid, while this stops the moment the work is no longer at risk, which is what ties it to contingency rather than to the calendar. And it is **bounded**.

The object multiplied is the whole argument. `r · U` prices unrecovered work. `cap × (1 + r)` prices money. The numbers are close and the objects are not, and only one of them is something a reader already has a name for.

On whether the administration would see this as interest: the framing to avoid is "would they notice". Plan for a reader who is right. The Dienst Voorafgaande Beslissingen looks at substance and naming will not move it, though the box can still be confirmed if the facts support it. The practical risk sits earlier and lower: a bookkeeper reaches for the nearest familiar object, puts the ceiling on a balance sheet, and turns the opening into a financial charge to a related party. After that the tax analysis follows the books whatever the annex says. So the ban on booking the ceiling is the clause that actually protects the characterisation, and it now has a written instruction to both accountants behind it.

One point worth holding on to: the size of `r` moves the risk without removing it. A rate near a plausible lending rate is the easiest to read as interest. A high `r` is harder to read as interest, because no lender earns that on a safe claim, but easier to attack as excessive under art. 53, 10°. That is the better of the two risks, because a partial disallowance is absorbed by the pool. It should be a chosen trade.

## Decisions

- The option-2 cap is one row per contributor; lots are retired for this path — [ADR 2026-09-14 one-row cap](../decisions/2026-09-14_simplified-cap-one-row.md).
- The opening is linear on unrecovered effort, with a lifetime lid.
- The "do not publish `r`" rule is split, not dropped: public and promotional material and any return framing stay banned; a contracted contributor may see their own row under stated limits.
- New prevention rule: [no cap as a balance times `(1 + r)`](../mistakes/2026-09-14_cap-as-balance-times-one-plus-r.md).

## Open Questions

- The values of `r` and `k`. `k` is now the only thing between this design and an unbounded ceiling, so it cannot stay open for ever.
- Whether a sunset `T` is used, and whether stopping the opening is the right shape for it (DVB **(g)**).
- Whether the contributor statement needs a fixed template before anyone receives one.
- Whether the DVB will answer the accounting question in **(h)** at all, or send it to an accountant.

## Next Steps

- Put the accounting question into the prefiling alongside **(h)**, not after it.
- Draft the written instruction to the accountant referred to in [annex-terms.md](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md) clause 27.
- Decide `k` with counsel before any contributor sees a statement.
