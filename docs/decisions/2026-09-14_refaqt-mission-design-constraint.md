# ADR — Refaqt mission is a binding design constraint

- **Date:** 2026-09-14
- **Status:** Accepted
- **Does not accept** option 2 yet; that remains the next pass.
- **Does not revive** cheap-share ([2026-09-04](2026-09-04_cheap-share-route-dead-end.md)), bonding-curve shares ([2026-09-07](2026-09-07_bonding-curve-shares-dead-end.md)), or *inbreng in nijverheid* ([2026-09-10](2026-09-10_inbreng-in-nijverheid-dead-end.md)).
- **Does not** choose Nationale Raad voor de Coöperatie recognition or *erkend als sociale onderneming*.

## Context

Token and legal design has been iterating on contribution credits, tax boxes, and company-law instruments without a written statement of **why Refaqt exists**. Belgian CV statutes need a *voorwerp* / *coöperatief doel* (art. 6:1 WVV). DVB item **(q)** needs a **non-tax reason** that would still hold if the tax outcome were reversed. FPS will read the shape of the scheme, not a slogan: if the only story is private profit extraction or a tax result, the administration can treat the arrangement as abuse.

The founder mission is manufacturing that uses less resources and energy by being more decentralized and local, more on-demand, and by democratizing access to manufacturing and manufacturing tools. QOLAB is an instrument of that mission, not a separate profit purpose.

Canonical text: [docs/mission.md](../mission.md). Session: [docs/log/2026-09-14_refaqt-mission.md](../log/2026-09-14_refaqt-mission.md).

## Decision

1. **Treat the mission as a binding constraint** on token-system, statute, DVB, and contract drafts. Check every sketch against [docs/mission.md](../mission.md). Reject drafts whose only story is private profit extraction or a tax result.
2. **Statutes, when drafted, must state this *doel* / *voorwerp*.** Dutch statutory wording is counsel, not this ADR.
3. **Surplus, membership, and instruments** should be narratable as serving that manufacturing mission (local, on-demand, less resource and energy use, democratized tools)—including why unallocated profit stays investable in the mission ([belgian-tax-and-company-law.md](../../token-system-design/analysis/belgian-tax-and-company-law.md) item 5).
4. The mission is a **non-tax rationale**, not a tax box, volunteer claim, or ruling. It does not convert contributors into volunteers, mix a dividend story and a fee on the same instrument, or revive labour-quota shares.

## Consequences

- Agents must read [docs/mission.md](../mission.md) before token or legal work ([`.agents-local/rules/repo.md`](../../.agents-local/rules/repo.md)).
- DVB **(q)** can cite the statutory mission, not only one-member-one-vote, as the independent reason for the company form and surplus policy.
- Counsel still drafts Dutch *statuten*. Recognition as a social enterprise remains a separate choice: art. 8:5 WVV’s ~6% cap on patrimonial advantage to shareholders fights a 10× residual.
- Operations have to match the text. A README does not make payments non-taxable.
