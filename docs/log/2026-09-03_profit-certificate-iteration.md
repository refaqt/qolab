# 2026-09-03 — Profit-certificate iteration vs Belgian tax

**Role(s):** finance, business-dev

## What happened

Reviewed `token-system-design/2026-09-03_token-system-calculation.ods` (bonding curve `p = c0 · c^k`, euro withdrawal rate `dc/dp`, GA pool, pro-rata opt-in, burn = cash / rate). Goals shifted to: reward voluntary contributions, early-bird, no tax at grant of the right, no unlimited dividends. Wrote [token-system-design/token-system.md](../../token-system-design/token-system.md). Restored [docs/architecture.md](../architecture.md) as a pointer to the working folder.

## Decisions

None accepted. Working recommendation: keep the mint curve and non-transferability; drop a published euro withdrawal rate; do not treat member volunteer work as a VAT/PIT exemption when certificates track contribution points; choose fee (option 2) or genuine dividend on a share class (option 1), not both on one instrument.

## Open Questions

- DVB on mint vs cash-out, and dividend vs fee characterisation.
- Whether contributors invoice as natural persons or via a BV (changes which option is cheaper).
- Pool as profit (GA, WVV tests) vs a capped revenue share.

## Next Steps

- Iterate the design (no PR yet). **Done for the `v = pool / N` trap:** [2026-09-03_vintage-pools-idle-capital.md](2026-09-03_vintage-pools-idle-capital.md).
- Counsel + accountant; then statutes vs dienstenovereenkomst.
