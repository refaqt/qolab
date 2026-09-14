# ADR — Two bases: the large multiple comes off the effort base

- **Date:** 2026-09-14
- **Status:** Proposed (pending counsel and a DVB prefiling). Nothing accepted as the live spec by this ADR.
- **Amends:** the working conclusion of the [2026-09-10 cap-opening discussion](../log/2026-09-10_pt-distribution-and-cap-opening.md) (gated `k = 10` on effort), which becomes **fallback B**; DVB item **(p)** becomes fallback-only.
- **Does not accept** the [scoped-royalty path](../../token-system-design/paths/scoped-royalty-cred-q/README.md) or [cash shares](../../token-system-design/paths/cash-shares-residual/README.md) as live. **Does not revive** cheap-share ([2026-09-04](2026-09-04_cheap-share-route-dead-end.md)), bonding-curve shares ([2026-09-07](2026-09-07_bonding-curve-shares-dead-end.md)), or *inbreng in nijverheid* ([2026-09-10](2026-09-10_inbreng-in-nijverheid-dead-end.md)). **Does not unpark** vintages.

## Context

The [2026-09-10 repo review](../log/2026-09-10_arms-length-10x-and-repo-review.md) found that the repo had built the large upside on the one base where it is hardest to defend. A ceiling written as `k × hours × frozen band` tells the administration the market price of the work (hours × rate); every euro above 1× must then be argued as a risk premium on a wage-like benchmark, every time. The same review found that the DVB rules on the legal treatment of a described transaction, not on quantum: expect the box ((a)–(e)) to be confirmed and `k` to come back as a condition (“provided the remuneration is at arm's length”), not a confirmation. Treating “DVB blesses 10×” as a launch gate waits for something that is unlikely to exist.

A royalty **scoped to the products that embody the contribution** is compared against royalty rates, where a 10× lifetime return on the effort is an ordinary outcome nobody computes. Cash-subscribed shares whose count is not `f(p)` carry upside as company value, which art. 53, 10° does not test. Both already exist in the repo as open sketches ([Cred/Q log](../log/2026-09-10_cred-value-q-euro-par.md), [tokens-not-shares §7](../log/2026-09-10_tokens-not-shares-avoid-revisor.md)). Failure mode if a large `k` on effort is later disallowed: the **CV** loses the excess deduction (art. 53, 10°, with the art. 206/3 §1 offset ban), the contributor is unchanged ([analysis §5](../../token-system-design/analysis/belgian-tax-and-company-law.md)).

Session: [2026-09-14 log](../log/2026-09-14_review-followups-and-path-restructure.md). Mistake: [2026-09-14 the multiple on the effort base](../mistakes/2026-09-14_10x-on-the-effort-base.md).

## Decision

Until counsel and a DVB prefiling say otherwise:

1. **Option 2 targets at or near 1× on documented effort** for ordinary time-based work. Lots, first-year 1×, freeze after 1× paid, the fractional burn and the nested machinery are unchanged; `k` stays a policy parameter but is small (worked examples use the older `k = 3` illustration at most). Do not spend the arm's-length fight there.
2. **The large upside lives on a different base:** a **scoped royalty** on the products that embody the contribution (Cred-allocated euro-par Q, [path note](../../token-system-design/paths/scoped-royalty-cred-q/README.md)), and/or **cash shares whose count is not `f(p)`** ([path note](../../token-system-design/paths/cash-shares-residual/README.md)). Two bases, two arm's-length tests (royalty rate; capital at risk), never on one instrument and never a share count or Cred share that is secretly `f(hours)`.
3. **Fallback B.** If the base is not moved, the gated `k = 10` path stays the honest way to argue a multiple as a success fee: file it as one ex-ante argument (expected value ≈ 1× because `P_t` may be zero and lots lapse unpaid), evidenced, with the disallowance allocation written ([annex terms](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md)), and accept that the number will not be confirmed.
4. **File for the box.** The gate before launch is DVB **(a)–(d)**; a decision that confirms the mechanism with arm's length as a condition is a success. **(s)** (scoped royalty) and **(q)** (art. 344 §1 on two instruments) are filed with whichever base is pursued.

## Consequences

- The Cred/Q sketch becomes a path note with a scoping rule, not a side log. The option-2 spec states its effort target and carries the 10× only as fallback B.
- Art. 344 §1 exposure of a two-instrument structure becomes live the moment a second base is pursued (DVB **(q)**): the share count or the royalty scope must have a non-tax reason that would hold if the tax outcome were reversed.
- The [path map](../../token-system-design/README.md) shows option 2 as live, scoped royalty as viable / proposed base, cash shares as open.
- Decision for the user and counsel: whether the goal survives moving the 10× off effort. If not, fallback B is the record, with its risks stated.
- No text anywhere publishes 10×, `r`, or ROI language.
