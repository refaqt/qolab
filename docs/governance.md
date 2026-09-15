# Governance

How Refaqt makes decisions. This is the operating model on top of the statutes. The statutes and the Code of Companies and Associations (WVV) set the hard limits; this document works inside them. The vote maths (share entitlement, decay, cap, veto share, asset lock) is in the [governance-voting path](../token-system-design/paths/governance-voting/README.md). Decision: [ADR 2026-09-15 (Proposed)](decisions/2026-09-15_votes-off-the-reward.md).

Status: **proposed**. Sections marked *to be defined* are open.

## 1. Layers

| Layer | Sets | Changed by |
| --- | --- | --- |
| Law (WVV) | What a CV may do; which decisions need a general assembly (GA), a special majority, or a notary | Parliament |
| Statutes | Mission, share classes, entitlement formula, vote cap, veto share, asset lock, GA rules | GA with a special majority; reserved matters also need the class G (veto) share |
| This document | Circles, decision rights, consent, escalation, hour acceptance | Consent in the general circle; ratified by the GA where the statutes require it |
| Circle policies | How one circle runs its domain | Consent in that circle, within its domain |

## 2. Objectives cascade

1. The **GA** decides the mission (in the statutes) and the **yearly key objectives**.
2. The general circle translates key objectives into **sub-objectives**.
3. Sub-objectives are grouped into **projects**. Each project circle splits its objectives into tasks.
4. Any member may propose a new project, or a change to sub-objectives that no longer fit the key objectives, at any time. **Budget** decisions between projects happen once a quarter, at the GA or in the general circle within the budget the GA set.

## 3. Decision rights

| Kind of decision | Who decides | How |
| --- | --- | --- |
| Operational work inside an accepted task | The member doing the work | Autonomously, in line with mission, objectives and sub-objectives |
| A plan the member doubts, or a plan that touches other people's work | The member, after advice | **Advice process:** ask the members best placed to advise; the advice is recorded; the member still decides |
| A policy, a role, a budget inside a circle's domain, or a tension between members | The circle that holds the domain | **Consent** (§4) |
| Mission, key objectives, budget split between projects, `P_t` policy, parameters `δ`, `k`, the cap floor, statutes, accounts, directors | The GA | Vote by governance shares, one share one vote, with the vote cap; reserved matters also need the class G share |
| Amount to distribute in a year (`P_t`) | The board, under the bound discretion in the option-2 spec | Not a vote; the split between legs is by formula |

Spend and commitment thresholds for autonomous decisions: *to be defined*.

## 4. Consent

A proposal names a **driver** (the tension or opportunity), the **change**, and the **impact** (who and what is affected, including budget and safety). The round is: clarifying questions → quick reactions → objections → integration.

- An **objection** is valid when the proposal would cause harm the role or circle cannot accept. A preference is not an objection.
- A proposal passes when there is no valid objection and it is **good enough for now and safe enough to try**.
- Every decision gets a **review date**. Policies are tests; they are reviewed and changed.
- Decisions are written down (this file, `docs/decisions/`, or the circle's own log).

## 5. Escalation ladder

When a circle cannot reach consent:

1. **Amend** the proposal to remove the harm the objection names.
2. **Try** the proposal with a short review date, if that is safe enough.
3. *When more than one circle exists:* **escalate** to the general circle through the double link.
4. **Vote** at the GA by governance shares.

At the start there is **one circle**. Its members are the members of the GA. The difference is legal, not personal: the circle decides by consent, and the GA acts under the statutes when the law or the statutes require a vote. Step 3 switches on when a second circle exists.

## 6. Circles

At the start: the **general circle** (all members). It holds every domain until it hands one to a project circle.

Planned, *to be defined*:

- **Project circles**, each with a domain description: purpose, scope, constraints, budget authority, spend thresholds.
- **Double links** between each project circle and the general circle (a leader chosen by the general circle and a representative chosen by the project circle).
- A **guardian circle**, which acts for the holder of the class G share, runs sample audits of the hours register, and holds the mission and asset lock.
- Selection of circle members and roles **by consent** (open nominations, reasons stated, no secret ballot). Circle membership is not decided by weighted vote.

## 7. Accepting hours

Accepted hours feed both the fee weights `p` and the governance share entitlement `N_i`. Rules:

- Nobody accepts their own hours.
- Hours are accepted by consent inside the project circle, against an accepted task.
- The register is published to members. There is an objection window before the yearly cut-off.
- At most 1,800 hours per member per year count for governance (parameter).
- The guardian circle runs sample audits.

A governance-distribution rule that does not rest on hours is *to be done* ([path note §4.5](../token-system-design/paths/governance-voting/README.md)).

## 8. What the GA must decide under the law

Some decisions are not valid as a chat poll or a consent round. The GA decides them under the statutes, sometimes with a special majority or a notary: approving the accounts, appointing directors, changing the statutes, issuing a new share class, merger, conversion, dissolution. A consent decision on those matters is a **proposal to the GA**, which then votes.

## 9. Membership

*To be defined:* admission conditions, exit, exclusion, mediation and conflict resolution, role terms, a decision log. Exit already has one fixed rule: all governance shares are withdrawn at €1 and `V_i` is set to zero; an option-2 row or a bond position follows its own table.

## 10. Review

This document is reviewed once a year, at the first GA after the cut-off date, together with the parameters `δ`, the divisor, `k` and the hours ceiling.
