# 2026-09-14 — Refaqt mission as a design constraint

**Role(s):** business-dev, finance

## What happened

Recorded Refaqt’s manufacturing mission so later token, statute, and DVB work is judged against it. Canonical text: [docs/mission.md](../mission.md). Accepted as a binding constraint: [ADR 2026-09-14](../decisions/2026-09-14_refaqt-mission-design-constraint.md).

The mission: make manufacturing use less resources and energy by making it more decentralized and local, more on-demand, and by democratizing access to manufacturing and manufacturing tools. QOLAB is an instrument of that mission, not a separate profit purpose.

Wired the same text into the always-read path (`.agents-local/rules/repo.md`, `AGENTS.md`, both architecture notes) so agents actually use it. Pointed [token-system.md](../../token-system-design/token-system.md) §3 and DVB item **(q)** at the mission as statutory *doel* / non-tax reason. Did not draft Dutch *statuten*.

## Decisions

Accepted: the mission is a binding design constraint ([ADR 2026-09-14](../decisions/2026-09-14_refaqt-mission-design-constraint.md)). Did not accept option 2, revive cheap-share, or choose *erkend als sociale onderneming*.

## Open Questions

- Dutch statutory wording of *voorwerp* / *doel* (counsel).
- Whether to seek NRC / *sociale onderneming* recognition despite art. 8:5 WVV’s ~6% cap.

## Next Steps

- Counsel: write the mission into draft statutes as *doel* / *voorwerp*.
- Keep checking token and DVB drafts against [docs/mission.md](../mission.md).
