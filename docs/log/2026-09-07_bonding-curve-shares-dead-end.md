# 2026-09-07 — Bonding-curve shares (dead-end)

**Role(s):** finance, business-dev

## What happened

Tried another option-1 path that keeps the value of contributions **constant and low** (like cheap shares) and still gives contributors a return. Contribution points mint **shares** on `p = c0 · c^k`; each point is booked at **€0.01**. Revenues also mint shares on the same curve. `k` is very small (~0.041, fitted so 50,000 points → 50,000 shares and 500,000 points → 55,000 shares) so price rises quickly.

Worked it in [token-system-design/2026-09-07_token-system-calculation.ods](../../token-system-design/2026-09-07_token-system-calculation.ods). After €400,000 revenue (2029-10-01, 400,000 points on the curve) the share price is €1.85:

| | Points | Shares minted | Multiple vs points-as-euros | Share value |
| --- | ---: | ---: | ---: | ---: |
| Alex (from 2027-01-01) | 2,002 | 43,763 | 40.5× | ~€81,136 |
| Bill | 7,000 | 2,592 | 0.69× | ~€4,806 |
| Christina | 10,000 | 1,682 | 0.31× | ~€3,119 |
| Revenue mint itself | 400,000 | ~6,562 | — | — |

The multiple has to be extremely large to climb out of the €0.01 grant value. That only happens if almost all shares mint at the origin, so later contributions (and the revenue mint) get a very low number of shares. Flattening `k` so later work still mints shares removes the price rise that was supposed to pay them. Unpractical. Rejected: [ADR 2026-09-07](../decisions/2026-09-07_bonding-curve-shares-dead-end.md). Logged in [docs/mistakes/2026-09-07_steep-curve-low-grant.md](../mistakes/2026-09-07_steep-curve-low-grant.md).

## Decisions

Rejected (dead-end): steep bonding-curve shares with a cheap constant contribution value and revenue minting on that curve. Still bound by the cheap-share rejection ([ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md)): labour-quota shares as the reward, and a published euro price per share. Next pass stays option 2 with less machinery.

## Next Steps

- Iterate option 2 with reduced complexity (not this curve, not cheap extra shares, not an `S − €` burn).
- Counsel + accountant after that simpler spec exists.
