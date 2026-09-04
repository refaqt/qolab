# 2026-09-04 — Fee cap is not a unit price of p

**Role(s):** finance, business-dev

## What happened

The vintage flow was read as: each year a pool `P_t` is split by share of `p`, and you cannot invoice more than `k ×` hourly rate `×` hours — so the price of `p` would be `(k × E) / Δp`, which would trigger VAT and tax at grant.

Wrote the distinction into [token-system-design/vintage-pools.md](../../token-system-design/vintage-pools.md) (effort ceiling vs unit FX vs ex-post return). Proposed [ADR 2026-09-04](../decisions/2026-09-04_fee-cap-not-unit-price.md). Added DVB item **(i)**. The reconstruction of the split-plus-clip is right; the quotient is not a property of `p`, and a ceiling is not consideration “to be received” while `P_t` may be zero. Still a hypothesis for DVB, not a ruling. Does not unpark vintages.

## Decisions

Proposed (not accepted): keep an effort-tied fee cap on the next option-2 pass; do not publish or book `(k × E) / Δp` as €/`p`; reject that arithmetic as the grant-time tax fact pattern. What still prices the mint: `w`, `v = P/N`, remaining `p` = remaining euros.

## Open Questions

- DVB (i): effort cap vs implied `€/p` at grant.
- How simple the next option-2 cap can be without a day-one `k×` that looks ascertainable when a fat year is forecasted.

## Next Steps

- Counsel + accountant on (i) with (a)–(d) and parked (e)–(h).
- Simpler option-2 spec; keep the cap on **work**, not on `p`.
