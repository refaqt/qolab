# ADR — Votes off the reward: √-count vote-only shares, a veto share, and an asset lock

- **Date:** 2026-09-15
- **Status:** Proposed (pending counsel). Nothing is issued, offered, or written into statutes by this ADR.
- **Amends:** decision 7 of [ADR 2026-09-14 investor leg](2026-09-14_investor-leg-capped-participating-bond.md) ("one member, one vote is written into the statutes for the general assembly") — replaced by one vote per governance share, with a per-member cap. Amends the "governance membership" constraint in the [path map](../../token-system-design/README.md) and the "same for each contributing member" wording in [publication-surfaces.md](../../token-system-design/paths/option-2-contingent-fee/publication-surfaces.md). Closes the open question in [mission.md](../mission.md) on recognition as *sociale onderneming*: **not sought**.
- **Does not change:** [option 2](../../token-system-design/paths/option-2-contingent-fee/README.md), the [capped participating bond](../../token-system-design/paths/capped-participating-bond/README.md), the split `θ`, or any ceiling. Nothing on this leg pays anyone.
- **Does not decide:** who holds the class G share before a foundation exists; the final values of `δ`, `k`, the divisor and the hours ceiling; a governance-distribution rule that does not rest on hours; circles beyond the first one; admission and exclusion rules.
- **Does not revive:** [cheap shares](2026-09-04_cheap-share-route-dead-end.md), [bonding-curve shares](2026-09-07_bonding-curve-shares-dead-end.md), or [*inbreng in nijverheid*](2026-09-10_inbreng-in-nijverheid-dead-end.md). The share here has no profit right, which is the fact those dead-ends turn on.

## Context

Every path in the repo pays a constituency. None says who votes. The repo had three one-line rules: the governance share is not the reward, share count never tracks contribution, and lenders have no vote. Refaqt is meant to be steward-owned: financial rights and voting rights are split, the residual belongs to the mission.

The user proposed contribution-weighted votes with yearly decay and a quadratic-style formula, plus a sociocratic operating model. The review ([2026-09-15 log](../log/2026-09-15_governance-token-and-sociocracy.md)) found: the formula was the Quadratic Funding formula without the proposal index; a square root taken per (member, proposal) rewards vote trading and spreading; a CV cannot issue a non-voting class (art. 6:19 WVV), which the bond already makes unnecessary; a share count that follows hours is only a problem when the share carries a profit right; and the entrenchment half of steward-ownership (veto share, asset lock) was missing. The user then chose share-count voting over register-weighted voting to keep the legal form at the WVV default.

## Decision

Until counsel says otherwise:

1. **One class of vote-only governance shares** at €1 each, non-transferable, no dividend, returned at €1 on withdrawal and at liquidation. Every member holds at least one.
2. **Share entitlement follows the square root of decayed contribution:** `V_i(n+1) = (1 − δ)·V_i(n) + c_i(n)` with `δ = 0.25` at the start; `N_i = max(1, ⌊√(V_i/1000)⌋)`. `c` is on the repo's scale (hours × 100). At most 1,800 hours per member per year count.
3. **Yearly rebalance with CV-native tools:** subscribe up to `N_i` at the cut-off; shares above `N_i` are withdrawn automatically at €1 (partial withdrawal, art. 6:120 WVV). No statutory vote-weighting formula, no register-based votes. The register's legal job is the subscription entitlement only.
4. **One share, one vote.** No vote spending. Binary decisions count shares per side. Budget splits let each member split their shares over the proposals; a proposal gets its share of the total.
5. **Vote cap** `cap(N) = max(10%, k/N)` of the votes present, `k = 2` at the start. Excess redistributed pro rata.
6. **Investors hold the bond and have no vote.** If a financial share class is ever created, it votes as a class with a ceiling (default 5% of votes present) and has no vote on reserved matters.
7. **A veto share** (class G, one share, held by a foundation or non-profit that is neither an investor nor a contributor) must approve: the mission; the rule that votes never attach to financial instruments; the entitlement formula and the parameters `δ`, divisor, `k`, cap floor; the asset lock and mission lock; sale, merger, conversion, dissolution; issuing any financial share class; its own terms.
8. **An asset lock and a mission lock in the statutes**, entrenched by the veto share: no dividend on the governance share, *scheidingsaandeel* at paid-in €1, no capital reduction to members, liquidation surplus to a like-purpose entity, proceeds of asset or IP sales stay inside the lock, designs stay open under CERN-OHL.
9. **Recognition as *sociale onderneming* is not sought.** The lock is statutory. Art. 8:5 WVV's cap on patrimonial advantage is no longer a design constraint.
10. **Operating model:** consent inside circles, one circle at the start, escalation ladder (amend → try with review date → escalate through the double link once a second circle exists → GA vote), circle members selected by consent, nobody accepts their own hours, consent outcomes on statutory matters are proposals the GA ratifies by vote. Details in [docs/governance.md](../governance.md).

## Consequences

- The compression of hours into votes is `√`: ten times the hours gives about three times the shares. At `δ = 0.25` the share half-life after a member stops contributing is about 4.8 years; a first-year member at the same rate holds half a veteran's shares. The tables in the [path note §2](../../token-system-design/paths/governance-voting/README.md) are the tool for tuning `δ` and `k`.
- No cross term and no spreading bonus, because the square root is taken once per member. Vote trading gains nothing.
- The statutory thresholds for a statute change, a quorum, and a class-rights change apply as written. The register never has to be proven to a notary.
- The accepted-hours register now decides both the fee weights and the share entitlement. It is the single point of control and gets the rules in [docs/governance.md §7](../governance.md).
- The path-map constraint changes from "share count never tracks contribution" to "share count never tracks contribution **on a share with a profit right**; the governance share has none". Nothing is minted from `p`; credits never become shares.
- The pair check passes: money flows from the member to the CV, so the share price cannot be consideration for work; no document states euros per hour or per `c`; lenders still have no vote.
- Steward-ownership is now complete on paper: capped capital, capped labour, residual to the mission, control with the people who work, entrenched by a veto share and an asset lock.
- New counsel items: entitlement and issuance clause; automatic partial withdrawal and the six-month window; vote cap; leonine minimum on a vote-only share; class G share and reserved matters; asset-lock and liquidation-destination clauses without recognition; class ceiling if a financial class ever exists.
