# 2026-09-03 — Time-opened fee cap vs vintage gold rush

**Role(s):** finance, business-dev

## What happened

The vintage option still paid a default `k × effort` from the first vintage, so a short payback (sudden success, large `P_t`) delivered the long-risk multiple. Forecasted revenue would pull contributions as a sure bet. Replaced the static ceiling with a per-lot **time-opened fee cap** (1× at first eligibility; opens with unpaid wait only; freeze after 1× is paid; record date `Y+1`). Wrote the three stories into [token-system-design/vintage-pools.md](../../token-system-design/vintage-pools.md). Proposed [ADR 2026-09-03](../decisions/2026-09-03_time-opened-fee-cap.md). Logged the failed approach in [docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md](../mistakes/2026-09-03_immediate-multiple-gold-rush.md).

## Decisions

Proposed (not accepted): lots, not a blended personal ceiling; record date; opened cap starts at 1×; `(1+r)` only while principal is unpaid, up to `k×`, then freeze; leftover still to reserves; no unit `v`; `r`/`k` are a fee cap, not a yield. Rejected as default: seniority waterfall, annual drip, coverage-based mint, age-opening after repayment.

## Open Questions

- Values of `k` and `r` (examples use 3 and 0.20).
- DVB (h): time-opened fee cap vs interest / receivable; still (e)–(g) from the vintage note.
- Whether junk-volume dilution later needs a junior/senior split of `P_t`.

## Next Steps

- Counsel + accountant on opened cap vs interest, and the existing vintage questions.
- Then draft the QOLAB regulation around vintages **and** the time-opened cap.
