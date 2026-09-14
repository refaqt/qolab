# 2026-09-14 — A cap written as a balance times `(1 + r)`

## What happened

A proposal to simplify the option-2 cap replaced the per-lot machinery with one running number per contributor:

```
cap(n+1) = cap(n) · (1 + r) + effort(n) − paid(n)      r = 0.25
```

The goal was right. A contributor should be able to answer "what may I still invoice?" from one row. The arithmetic was wrong, and it was caught before it reached the spec.

## Why it went wrong

The formula grows a **balance**. That is the arithmetic of a loan, and it takes three things away at once.

- **It never stops.** There is no lid, so the ceiling reaches about 9 times documented effort after ten unpaid years, about 87 times after twenty, and about 808 times after thirty. Option 2 aims at or near 1 times documented effort.
- **It never freezes.** The growth applies to the whole balance, including the part left over after the work has been paid in full. Pay someone €10,000 in full and they keep €2,500, then €3,125, then €3,906, growing every year on work that is no longer at risk. This is the trailing coupon the repo had already rejected once.
- **It stops the weights from retiring.** Weight burns by `p · alloc / rem`. If `rem` grows without a bound, the fraction burned per euro falls towards zero. The person who waits longest ends up with both the largest ceiling and the most durable weight in every later split.

The deeper problem is what the formula multiplies. Interest is the price of using a sum of money. If the design multiplies a **balance**, a reader already has a name for the result, and the name is a loan. The two facts that make the opening defensible as a fee bound — it stops when the work stops being at risk, and it is bounded — are exactly the two facts this form removes.

## Prevention rule

Never write a fee ceiling as a running balance multiplied by `(1 + r)`.

Write the opening as a factor on **unrecovered documented effort**: `O += r · U`, where `U` is documented work that was already on the books at the start of the period and is still not covered at its end. Keep a lifetime lid `cap ≤ k · E`. Then the one-period gate on new work, the stop once the work is paid, and the bound all follow from the formula instead of being separate rules that someone can drop.

Say what the factor multiplies whenever the factor appears. Publish a tariff on unpaid work, never a rate on a balance. Do not let the ceiling be booked: once it is on a balance sheet, the opening is a financial charge and the tax analysis follows the books, whatever the contract says.

## Related

- [docs/decisions/2026-09-14_simplified-cap-one-row.md](../decisions/2026-09-14_simplified-cap-one-row.md)
- [token-system-design/paths/option-2-contingent-fee/README.md](../../token-system-design/paths/option-2-contingent-fee/README.md)
- [token-system-design/analysis/dvb-questions.md](../../token-system-design/analysis/dvb-questions.md)
- [docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md](2026-09-03_immediate-multiple-gold-rush.md)
- [docs/mistakes/2026-09-08_unburned-p-after-cap.md](2026-09-08_unburned-p-after-cap.md)
