# 2026-09-03 — Immediate lifetime multiple on a vintage

## What happened

The vintage design paid `pay_i = min(gross_i, k × documented effort − already_paid)` with that `k×` open from the first vintage. Good years were supposed to “hit the ceiling sooner.” When a large `P_t` is foreseeable, people contribute to lock in that multiple on a short payback.

## Why it went wrong

The multiple was meant to compensate risk and waiting. A static cap does not measure either. Forecasted revenue then makes contributing a near-certain high multiple. The mint curve does not stop this: late work still mints weight and shares the fat vintage. A per-person blend lets new lots inherit old waiting.

## Prevention rule

Do not open a lifetime multiple on day one. Cap each **lot** at 1× documented effort at first eligibility; raise the cap only while that lot’s principal is unpaid, then freeze once 1× is paid. Lots minted in year `Y` first sit in vintage `Y+1`. Do not advertise `r` or `k` as a target return.

## Related

- [token-system-design/vintage-pools.md](../../token-system-design/vintage-pools.md)
- [docs/decisions/2026-09-03_time-opened-fee-cap.md](../decisions/2026-09-03_time-opened-fee-cap.md)
- [docs/mistakes/2026-09-03_unit-price-on-growing-pool.md](2026-09-03_unit-price-on-growing-pool.md)
