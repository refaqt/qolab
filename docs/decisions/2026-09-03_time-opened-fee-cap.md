# ADR — Time-opened fee cap (no default k× on a short payback)

- **Date:** 2026-09-03
- **Status:** Proposed
- **Amends:** fee-cap mechanics in [2026-09-03 vintage pools](2026-09-03_vintage-pools-no-unit-price.md) (point 4) and the personal-cap line in [2026-09-02](2026-09-02_tax-aware-contribution-credits.md) (point 5). Both still proposed. Does not accept option 1 vs 2.

## Context

Vintages stop wait-and-run: each year a budget `P_t`, default-in, no burn, leftover to reserves. They still handed every contributor a lifetime ceiling `k × documented effort` from the first vintage. A sudden fat `P_t` fills that multiple in one invoice. When a boom is forecasted, contributing is a sure bet on a high multiple — even if the payback period is a few months.

The mint curve `p = c0 · c^k` only changes weight. A late lot still mints `Δp` and races to the same `k×`. A blended per-person ceiling lets last week’s work inherit years of “waited” cap.

Full note: [token-system-design/vintage-pools.md](../../token-system-design/vintage-pools.md) (time-opened cap and the three worked stories).

## Decision

Until counsel and an accountant say otherwise:

1. Track **lots** (mint event / contribution year), not one blended ceiling per person.
2. **Record date:** lots minted in fiscal year `Y` first sit in vintage `Y+1`.
3. **Opened cap starts at 1×** documented effort `E_L` (hours × frozen contractor band, or a task estimate).
4. At the start of each later vintage, if `paid_L < E_L`: `cap_L = min(k × E_L, cap_L × (1+r))`. If `paid_L ≥ E_L`, **freeze** `cap_L`. No trailing bonus after a short payback.
5. `pay_i = min(gross_i, Σ remaining_L)` with `remaining_L = cap_L − paid_L`. Allocate oldest unpaid lot first. Leftover of `P_t` still goes to **operating reserves**.
6. `k` and `r` are GA/board policy. They are a **fee cap**, not a published return. Do not book `cap_L` as a growing receivable. Worked examples use `k = 3`, `r = 0.20` as parameters, not a promise.
7. Sunset `T` may sit on top. It does not replace the opened cap.
8. Do not use a seniority waterfall, a fixed annual drip, a coverage-based mint, or age-opening after repayment as the default.

## Consequences

- Short payback pays about 1×; leftover of a fat vintage stays at Refaqt.
- Long unpaid wait can still reach toward `k×`. That is the risk premium.
- A forecasted boom is a sure bet on getting paid for work, not on `k×`.
- Same-year invoiced vintages and the no-unit-`v` rules are unchanged.
- Do not describe `r` as interest. DVB item **(h):** time-opened fee cap vs interest / receivable.
- Next step: human review of (e)–(h), then regulation text.
