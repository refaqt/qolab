# 2026-09-04 — Uniform points per hour as a weight scale

**Role(s):** finance, business-dev

## What happened

Asked whether minting contribution points from time spent risks a euro reclassification: if everyone gets 100 points per committed hour, and the industry rate for the work is €100/hour, would FPS treat 1 point as €1 and therefore give `p` a euro value at grant?

## Decisions

Proposed (not accepted): **100 points per hour for every contributor is fine as a weight scale.** It only renames hours. It does not by itself give points or `p` a euro value.

What still prices the points (and then infects `p`) is coupling that scale to a market wage — e.g. choosing 100 points/hour *because* the job is €100/hour, or writing industry €/hour into the points rule. Keep industry rates **off** the points rule. Hours × a contractor band stay an **invoice ceiling** at cash-out, not a grant-time FX. Related: [ADR 2026-09-04 fee cap is not a unit price of `p`](../decisions/2026-09-04_fee-cap-not-unit-price.md).

Time-based points are still **labour**, not a volunteer or dividend story. Option 1 stays the weak box. Next pass remains option 2.

## Open Questions

- DVB (i) should also cover this variant: if points are a linear function of hours and a market wage exists, is that a taxable amount at mint even with no published `€/p`?

## Next Steps

- Keep a uniform points-per-hour weight in the simpler option-2 spec; do not calibrate it to salaries.
- Counsel + accountant on (i), including this hours-only mint.
