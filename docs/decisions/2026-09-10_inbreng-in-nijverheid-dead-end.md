# ADR — Inbreng in nijverheid is a dead-end

- **Date:** 2026-09-10
- **Status:** Rejected (dead-end)
- **Does not accept** option 2 yet; that remains the next pass.
- **Does not revive** cheap-share ([2026-09-04](2026-09-04_cheap-share-route-dead-end.md)) or bonding-curve shares ([2026-09-07](2026-09-07_bonding-curve-shares-dead-end.md)).
- **Amends:** payout / wrapper comments in [2026-09-02](2026-09-02_tax-aware-contribution-credits.md) (still proposed). Confirms option 1 via labour-for-shares is not a way out when reward is meant to come **after** unplanned work.
- **Closes** the “honest nijverheid instead of a revisor on every task” fork discussed under [tokens not shares](../log/2026-09-10_tokens-not-shares-avoid-revisor.md). That log stays open for **contract** tokens / two-instrument residual; it is not a path to nijverheid shares.

## Context

Asked whether contributors could obtain shares through *inbreng in nijverheid* (art. 1:8 WVV) without a bedrijfsrevisor on every contribution: approve **hours × rate** once and apply it whenever shares unlock; or send a list of work, hours, and shares. The intended product is to **reward later**, after work is done, **without** people planning who will contribute, at which rate, and for how many hours.

Company law does not fit that product. *Inbreng in nijverheid* is a **commitment to perform work**. The board and the revisor must describe and value **each** contribution **before** shares exist (CV: arts. 6:8 / 6:110). A method is not a standing licence. Delivery afterwards is *volstorting*, not the valuation. A yearly batch still needs names, bounded commitments, and rates for that round. Hours × rate is also a grant-time euro value.

Session: [docs/log/2026-09-10_inbreng-in-nijverheid-dead-end.md](../log/2026-09-10_inbreng-in-nijverheid-dead-end.md).

## Decision

1. **Reject** *inbreng in nijverheid* as the path that unlocks shares for QOLAB contributions. Do not implement it. Do not promise shares against a work commitment or a timesheet.
2. **Reject** the lightenings that were asked: one-time method approval; a post-hoc list to the revisor; issue-then-check hours. None of those replace the per-issuance reports.
3. **Next pass:** option 2 (contingent invoiced fee, points as weights) with **reduced complexity**. Constraints that still bind: no euro par on `p`; no `v = pool / N`; an effort-tied fee cap is **not** a unit price of `p` ([ADR 2026-09-04](2026-09-04_fee-cap-not-unit-price.md)); do not mix dividend and fee on one instrument; governance share ≠ reward; **do not issue (or convert into) shares for the work**.

## Consequences

- The only nijverheid sequence that is legally light (one bounded future commitment per person, valued once) is the one QOLAB does **not** want: plan hours and rates **beforehand**.
- The sequence QOLAB wants (work first, reward later, open membership, no headcount plan) is a **fee / credit** story, or cash-issued shares whose **count is not** `f(hours)`.
- Honest nijverheid remains a share-valuation event — often worse than a contingent fee — plus lapse / non-compete overlay (art. 6:11 WVV). It is not a shelter and not a lighter revisor.
- Next write-up should stay on simpler option 2, not another labour-for-shares wrapper.
