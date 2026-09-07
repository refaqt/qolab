# 2026-09-07 — Steep bonding curve vs low grant-time contribution value

## What happened

Tried to keep contribution value constant and low (€0.01 per point, like cheap shares) and still give contributors a return by minting shares on a steep bonding curve (`k` ~ 0.041) and letting revenues mint on the same curve.

## Why it went wrong

A small `k` makes price rise quickly **because almost all shares mint at the origin**. In the worked sheet, Alex’s first 2,000 points minted ~43,763 shares; Bill’s 7,000 points minted ~2,592; Christina’s 10,000 points minted ~1,682; €400,000 of revenue minted only ~6,562. After that revenue, Alex’s multiple vs points-as-euros was 40.5×; Bill 0.69×; Christina 0.31×. The multiple needed to overcome the cheap grant value is extreme and unpractical. Flattening the curve so later work still mints shares removes the price rise. The sketch also publishes a euro price per share and still uses labour-quota shares as the reward.

## Prevention rule

Do not combine a low constant grant-time contribution value with a steep bonding curve (and revenue minting on that curve) to manufacture a return. Those three goals conflict: the curve that pumps price mints almost all shares up front; a usable later mint needs a flatter curve, which then cannot climb out of the cheap grant value. Do not issue extra shares whose number is set by contribution points. Do not publish a euro price per share.

## Related

- [token-system-design/2026-09-07_token-system-calculation.ods](../../token-system-design/2026-09-07_token-system-calculation.ods)
- [docs/log/2026-09-07_bonding-curve-shares-dead-end.md](../log/2026-09-07_bonding-curve-shares-dead-end.md)
- [docs/decisions/2026-09-07_bonding-curve-shares-dead-end.md](../decisions/2026-09-07_bonding-curve-shares-dead-end.md)
- [docs/mistakes/2026-09-04_cheap-share-euro-par.md](2026-09-04_cheap-share-euro-par.md)
- [docs/mistakes/2026-09-03_unit-price-on-growing-pool.md](2026-09-03_unit-price-on-growing-pool.md)
- [docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md](2026-09-03_immediate-multiple-gold-rush.md)
