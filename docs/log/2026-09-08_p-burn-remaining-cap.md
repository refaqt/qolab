# 2026-09-08 — Proportional burn of `p` against remaining opened cap

**Role(s):** finance, business-dev

## What happened

Without burning `p`, large contributors whose caps were already filled still held historical weight. After everyone contributed again — same point on the global bonding curve, same new risk — veterans took much more of every later vintage than newcomers. Accepted burn: `p_i · (revenue_i / remaining opened cap_i)` (allocation before payout; `rem = 0` ⇒ `p = 0`). Not a euro par. Wrote [token-system-design/p-burn-remaining-cap.md](../../token-system-design/p-burn-remaining-cap.md), [ADR 2026-09-08](../decisions/2026-09-08_p-burn-remaining-cap.md), and [mistake 2026-09-08](../mistakes/2026-09-08_unburned-p-after-cap.md).

## Decisions

Accepted (design): amortize `p` against remaining opened cap each vintage; haircut on allocated amount (including forfeit); apply from the start so new work mints onto `p = 0` after a filled cap. Still rejected: `w`, `v = pool / N`, 1 `p` = €1, `S ← S − €`. Vintage lots stay parked; if they return, same fraction per lot. DVB **(j)** added.

## Open Questions

- DVB (j): remaining `p` linear in remaining opened cap vs remaining consideration at grant.
- Whether a per-person blend is enough, or lots are needed when people add work while `rem > 0`.

## Next Steps

- Keep this burn in the option-2 spec.
- Counsel + accountant on (a)–(d), (h), (i), and (j).
