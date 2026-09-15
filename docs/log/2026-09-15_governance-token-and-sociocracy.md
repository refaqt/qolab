# 2026-09-15 — Governance leg: contribution-weighted votes, steward-ownership, sociocracy

**Role(s):** finance, business-dev

**Status:** Proposed. New path: [governance-voting](../../token-system-design/paths/governance-voting/README.md). Decision: [ADR 2026-09-15](../decisions/2026-09-15_votes-off-the-reward.md). Operating model: [docs/governance.md](../governance.md). Design input for counsel, not a ruling.

**Prevention rules applied:** [no labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md) — the governance share has no profit right; [a second instrument must not publish the comparable](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md) — pair check in the path note §6; [no euro spot price on contribution](../mistakes/2026-09-03_unit-price-on-growing-pool.md) — no euros per hour or per point anywhere.

## What happened

Reviewed the user's proposal for the governance side of QOLAB. Until now the repo only had the financing side. The proposal: log hours `c_i`; let contributors buy cheap shares in proportion to hours; the shares have votes only; a yearly halving `V(n+1) = V(n)/2 + c(n)`; voting by `P_l = (Σ √V_i)²`, `G_l = P_l / Σ P_l`; and a sociocratic operating model (objectives cascade, autonomy, advice, consent, an expert-group vote as fallback). The user asked what the gaps were and whether the formula matched Quadratic Funding.

### 1. Formula check

- `P_l = (Σ_i √V_i)²` is the Quadratic Funding formula (Buterin, Hitzig, Weyl), but QF sums `√(c_i^l)` — what member `i` puts on proposal `l`. Without the `l` index every proposal scores the same.
- Quadratic voting is different again: `v` votes cost `v²` credits, tally `Σ √(credits_i^l)`, no outer square. The outer square is QF's matching device.
- Both put the square root per (member, proposal). In a small cooperative that gives (a) a cross term `2√(ab)` that pays two members to trade votes (worked example: members 16 / 16 / 4, sincere 44 / 44 / 11% → colluding 47 / 47 / 6%), and (b) a spreading bonus: one member splitting over two proposals gets `1.41 √V` of weight.
- Fix: take the square root **once per member**, then linear. The user chose to put that square root in the **number of shares**: `N_i = ⌊√(V_i/1000)⌋`, one share one vote. Same example with shares 4 / 4 / 2: sincere 40 / 40 / 20%, colluding 40 / 40 / 20%.
- No vote spending. Decay is a parameter `δ`: `V(n+1) = (1 − δ)·V(n) + c(n)`, start `δ = 0.25`. Under the square root, shares fall by `√0.75 = 0.87` a year when contribution stops (half-life 4.8 years); steady state `V = 4c`; a first-year member holds half a veteran's shares.

### 2. Company law

- A CV can only issue voting shares and bonds (art. 6:19 WVV), so "only one class votes" is not writable. The design does not need it: investors hold the bond and have no vote. If a financial class is ever created, it gets a class ceiling (default 5% of votes present).
- Share count following hours is only the dead-end fact when the share has a profit right. A vote-only share at €1, returned at €1, transfers no value. The leonine rule needs the €1 back; counsel confirms.
- Reducing share counts by selling back each year was replaced by automatic partial withdrawal at the cut-off (art. 6:120 WVV). Issuing extra shares to members needs no statute change in a CV.
- Register-weighted voting (one share per member, statutory formula) was proposed first and withdrawn by the user: it needs a weighting formula in the statutes, a register with evidentiary status, and quorum work. Share count keeps the WVV default.
- Vote cap `cap(N) = max(10%, k/N)`, `k = 2`: the 10% floor takes over from 20 members; below that the founders' weight difference survives. Recognition by the Nationale Raad voor de Coöperatie is not the reason; the cap is our own rule.
- The accepted-hours register now feeds both the fee weights and the share entitlement. Rules: nobody accepts their own hours; acceptance by consent against an accepted task; published register with an objection window; 1,800-hour yearly ceiling; sample audits.

### 3. Steward-ownership

The capped bond, the capped fee and the residual to the mission already give the "profits serve purpose" half. Missing: a **veto share** (class G, held by a foundation or non-profit, approval required on reserved matters) and an **asset lock** with a **mission lock** (no dividend on the governance share, €1 *scheidingsaandeel*, liquidation surplus to a like-purpose entity, IP proceeds stay locked, designs stay open under CERN-OHL, lock on the lock). The user added both. Recognition as *sociale onderneming* is not sought; the lock is statutory and its strength is its entrenchment.

### 4. Sociocracy

Matches: cascade mission → objectives → projects, autonomy in role, advice process, consent with "good enough for now, safe enough to try". Departures fixed: the escalation ladder ends in a vote instead of starting with one (amend → try with review date → escalate through the double link → GA vote); the decision domain belongs to the circle, and circle members are selected by consent rather than by weighted vote; a consent outcome on a statutory matter is a proposal the GA ratifies; hour acceptance is itself a decision with a conflict rule. One circle at the start.

## Decisions

Proposed, in [ADR 2026-09-15](../decisions/2026-09-15_votes-off-the-reward.md): vote-only governance shares at €1 with `N_i = max(1, ⌊√(V_i/1000)⌋)`; `δ = 0.25`; one share one vote; no spending; vote cap `max(10%, 2/N)`; investors on the bond with no vote; veto share; asset lock and mission lock; no *sociale onderneming* recognition; consent inside one circle with the escalation ladder. Amends decision 7 of the [investor-leg ADR](../decisions/2026-09-14_investor-leg-capped-participating-bond.md) (one member, one vote) and the path-map constraint on share count.

## Open Questions

- Counsel: entitlement and issuance clause; automatic partial withdrawal and the six-month window; vote-cap clause; leonine minimum; class G share and reserved matters; asset-lock and liquidation-destination clauses; class ceiling if a financial class ever exists.
- Who holds the class G share before a foundation exists.
- Whether `δ = 0.25` and `k = 2` are the right start values.
- **To be done:** a governance-distribution rule that does not rest on hours (self-election versus exclusion dilemma).
- **To be done:** circles beyond the first, domain descriptions, double links; admission, exit, exclusion; mediation; review dates and role terms; spend thresholds; a decision log.

## Next Steps

- Counsel on the items above before any statutes are drafted.
- Decide the class G holder.
- Run the §2 tables of the path note with real member numbers once there are members, and tune `δ` and `k` at the first yearly review.
