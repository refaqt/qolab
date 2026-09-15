# Governance leg — √-count vote-only shares, veto share, asset lock (open)

**Status: open (proposed).** This is the first path that describes **who votes, with how many votes**. Every other path pays people. This one does not pay anyone. A member buys vote-only shares at €1 each. The number of shares a member may hold follows the **square root** of their decayed contribution. One share is one vote. A per-member vote cap, a veto share held by a foundation, and an asset lock complete the steward-ownership shape. It is a **pre-legal spec**: every company-law statement below is a counsel item, not a checked article.

**Prevention rules applied:** [no labour-quota cheap shares as a dividend](../../../docs/mistakes/2026-09-04_cheap-share-euro-par.md) — the share here carries **no** profit right, which is the fact that rule is about; [a second instrument must not publish the comparable the first is designed not to have](../../../docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md) — §6 runs the pair check; [no euro spot price on contribution](../../../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md) — no document states a price per hour or per point.

Decision: [ADR 2026-09-15 votes off the reward (Proposed)](../../../docs/decisions/2026-09-15_votes-off-the-reward.md). Operating model (circles, consent, escalation): [docs/governance.md](../../../docs/governance.md). Working notes and the formula review: [2026-09-15 log](../../../docs/log/2026-09-15_governance-token-and-sociocracy.md). Symbols: [glossary.md](../../glossary.md). Counsel items: [dvb-questions.md § Counsel items](../../analysis/dvb-questions.md#counsel-items-not-numbered-dvb-items). The labour leg is [option 2](../option-2-contingent-fee/README.md); the capital leg is the [capped participating bond](../capped-participating-bond/README.md).

---

## Direct answers

| Question | Working answer |
| --- | --- |
| Can a CV have one share class that votes and one that does not? | **No.** A CV may only issue voting shares and bonds (art. 6:19 WVV). The design does not need a non-voting class: **investors hold the bond and have no vote at all.** There is one share class for governance. If a financial share class is ever created ([cash-shares path](../cash-shares-residual/README.md)), the statutes cap that class at a small share of the votes (§4.1). |
| Does "share count follows hours" reopen the cheap-share dead-end? | **No, because the share carries no profit right.** The dead-end is about *dividend* shares whose number tracks work. A vote-only share bought at €1 and returned at €1 transfers no value. Subscribing to it is not a benefit for the work. Counsel confirms that the €1 back on exit is enough participation to satisfy the leonine rule (art. 4:2 WVV). |
| Is the formula quadratic voting or quadratic funding? | **Neither, and that is on purpose.** Both apply a square root per (member, proposal). That rewards spreading and vote trading (§3). Here the square root is taken **once per member**, in the number of shares. After that everything is linear: one share, one vote. |
| Why not weight votes by a register instead of by shares? | It is possible but needs a statutory weighting formula, a register with legal status, and counsel work on quorums. Voting by share count is the WVV default and needs none of that. The register only decides **how many shares a member may subscribe**, which is an admission rule. |
| How do share counts go down when contribution stops? | Through the CV's own tool for a member taking back part of their shares (*gedeeltelijke terugneming van aandelen*, art. 6:120 WVV), made automatic in the statutes at the yearly cut-off, at the €1 *scheidingsaandeel*. With the default decay this only bites for members whose contribution drops. |
| Is this the reward? | **No.** Nothing here pays anyone. The reward for work stays on [option 2](../option-2-contingent-fee/README.md). Votes never sit on the fee or on the bond. |

---

## 1. Mechanism

### 1.1 Contribution register and decay

`c_i(n)` is the contribution of member `i` accepted in year `n`, on the repo's scale (`c = hours × 100`, [glossary](../../glossary.md)). The same accepted hours feed the option-2 weights `p`. Only hours accepted against a task in a project count. A yearly ceiling on hours that count for governance (parameter, default 1,800) stops padding.

```
V_i(n+1) = (1 − δ) · V_i(n) + c_i(n)        δ = 0.25 at the start (GA parameter)
```

`V_i` is a decayed stock of contribution. With `δ = 0.25`, 75% of last year's `V` carries over. Recent work counts more than old work. `V` is **not** a claim on anything; it only sets the share entitlement below.

### 1.2 Share entitlement

```
N_i(n) = max( 1, ⌊ √( V_i(n) / 1000 ) ⌋ )
```

`N_i` is the number of governance shares member `i` may hold in year `n`. Each share costs €1 and is returned at €1. The square root is taken here, once, and nowhere else. The divisor 1000 is a scale parameter (`V/1000` is decayed hours divided by 10).

### 1.3 Yearly rebalance

At the yearly cut-off date:

1. The register keeper publishes `V_i` and `N_i` for every member. Members have an objection window.
2. Each member may **subscribe** up to `N_i` shares at €1 each (cash in; *inbreng in geld*; no revisor). A CV can issue extra shares to existing members and admit new members without changing the statutes, within the rule the statutes set.
3. Shares above `N_i` are **withdrawn automatically** at €1 each (partial withdrawal, art. 6:120 WVV, written as a statutory rule tied to the entitlement). The net-asset and liquidity tests apply to that payment; the amounts are tens of euros, and payment is delayed if a test fails.
4. Every member keeps at least one share while they are a member.

Nobody has to sell anything to anyone. The register never carries a vote; it carries an entitlement to subscribe.

### 1.4 Voting

- **One share, one vote** (the WVV default). No statutory weighting formula.
- **Binary decision:** votes for = shares voting for; votes against = shares voting against.
- **Budget split between `L` proposals:** each member splits their shares over the proposals (whole shares). `S_l = Σ_i s_i^l`, and proposal `l` gets `G_l = S_l / Σ_l S_l` of the budget. A "reserve / none of these" bucket is always on the list.
- **No spending.** Voting never uses up shares or `V`.
- **Vote cap:** no member may cast more than `cap(N)` of the votes present or represented, with `N` the number of members:

```
cap(N) = max( 10%, k / N )        k = 2 at the start (GA parameter)
```

The cap is the classic cooperative clause "no member votes for more than X%". Votes above the cap are redistributed pro rata. With `k = 2` the 10% floor takes over from 20 members. Below that, nobody holds more than twice an equal share, so the founders' difference in weight survives without one person holding a majority alone.

### 1.5 Parameters

| Parameter | Start value | Set by | What it does |
| --- | --- | --- | --- |
| `δ` | 0.25 | GA | Yearly decay of `V` (share of `V` that drops off) |
| divisor | 1000 | GA | Scale between `V` and share count |
| share price | €1 | statutes | Cash per share; also the amount returned |
| hours ceiling | 1,800 / year | GA | Maximum hours per member that count for `V` in a year |
| `k` | 2 | GA | Vote cap `max(10%, k/N)` |
| cap floor | 10% | statutes | Lower bound of the cap once membership is large |

Changing `δ`, the divisor, `k`, or the cap floor needs the veto share's approval (§5.1).

---

## 2. Worked numbers

All tables use `c = hours × 100`, `δ = 0.25`, divisor 1000.

### 2.1 Shares by hours per year

Steady state means the member has contributed at that rate for many years (`V = c / δ = 4c`).

| Hours / year | `c` | First-year `V` | First-year shares | Steady-state `V` | Steady-state shares |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 100 | 10,000 | 10,000 | 3 | 40,000 | 6 |
| 200 | 20,000 | 20,000 | 4 | 80,000 | 8 |
| 500 | 50,000 | 50,000 | 7 | 200,000 | 14 |
| 1,000 | 100,000 | 100,000 | 10 | 400,000 | 20 |
| 1,500 | 150,000 | 150,000 | 12 | 600,000 | 24 |
| 2,000 | 200,000 | 200,000 | 14 | 800,000 | 28 |

Ten times the hours gives about three times the shares. A first-year member at the same rate holds half the shares of a long-time member.

### 2.2 What `δ` does

| `δ` | `V` kept per year | Shares kept per year when contribution stops (`√(1−δ)`) | Share half-life | Steady state `V` | First-year member vs veteran |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 0.25 | 0.75 | 0.87 | 4.8 years | 4.00 `c` | 0.50 |
| 0.50 | 0.50 | 0.71 | 2.0 years | 2.00 `c` | 0.71 |
| 0.75 | 0.25 | 0.50 | 1.0 year | 1.33 `c` | 0.87 |

Because of the square root, shares fall more slowly than `V`. Pick `δ` by the share half-life you want, not by the `V` half-life.

### 2.3 One member over time

A member contributes 1,000 hours a year for five years, then stops.

| Year | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| `V` (thousands) | 100 | 175 | 231 | 273 | 305 | 229 | 172 | 129 | 97 | 72 | 54 |
| Shares | 10 | 13 | 15 | 16 | 17 | 15 | 13 | 11 | 9 | 8 | 7 |

In years 2–5 the member subscribes 3, 2, 1 and 1 extra shares. From year 6 the CV withdraws 2, 2, 2, 2, 1 and 1 shares a year at €1 each. Six years after stopping, the member still holds 7 of 17 shares. That is the intended memory of past work at `δ = 0.25`.

### 2.4 Vote cap by membership size

| Members `N` | 3 | 5 | 10 | 20 | 30 | 50 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| `cap`, `k = 2` | 67% | 40% | 20% | 10% | 10% | 10% |
| `cap`, `k = 3` | 100% | 60% | 30% | 15% | 10% | 10% |

---

## 3. Why the square root sits in the share count

The user's first sketch used `P_l = (Σ_i √V_i)²` and `G_l = P_l / Σ_l P_l`. That is the **Quadratic Funding** formula (Buterin, Hitzig, Weyl, *Liberal Radicalism*), with one change: QF sums `√(c_i^l)`, the amount member `i` puts on proposal `l`. Without the `l` index every proposal gets the same score. **Quadratic voting** (Lalley, Weyl) is a different object again: `v` votes cost `v²` credits, and the tally is `Σ_i √(credits_i^l)` with **no outer square**. The outer square is QF's matching device: it makes broad support count more than linearly (four people with 1 each give 16; one person with 4 gives 4).

Both formulas put the square root **per (member, proposal)**. In a small cooperative with named members that causes two problems:

1. **Cross term (QF only).** `(√a + √b)² = a + b + 2√(ab)`. The extra `2√(ab)` only appears when two *different* members back the same proposal. On the open internet that is the signal QF wants. In a room of 10 to 50 members, breadth is already visible, and the cross term simply pays members to trade votes. Example with three proposals and members A (16), B (16), C (4): sincere voting A→1, B→2, C→3 gives 44% / 44% / 11%. If A and B each put half on proposal 1 and half on proposal 2: `(√8 + √8)² = 32` each, so 47% / 47% / 6%. C lost a third of its budget share; nobody's real preference changed. Gitcoin's pairwise-bounded and cluster matching are patches for exactly this.
2. **Spreading bonus (QF and QV).** One member who splits `V` over two proposals gets `2√(V/2) = 1.41 √V` of total weight instead of `√V`. Spreading thinly inflates influence even without a partner.

**The fix is to take the square root once, per member, and go linear after that.** Here the square root is the share entitlement `N_i = ⌊√(V_i/1000)⌋`. From then on shares add linearly. Repeat the example with shares 4, 4, 2: sincere gives 40% / 40% / 20%; A and B splitting gives 40% / 40% / 20%. No cross term, no spreading bonus. The compression is still there: four times the hours gives twice the shares. This is **square-root-count voting**, not QV and not QF. If a bonus for broad support is ever wanted, add it as a separate, explicit rule; do not get it by accident from a formula.

---

## 4. Company law

### 4.1 All CV shares vote

A CV may issue only registered voting shares and bonds (art. 6:19 WVV). A non-voting financial class is not available, and the design does not need one: the investor leg is a bond, and lenders have no GA vote ([bond path §5.4](../capped-participating-bond/README.md)). If the [cash-shares path](../cash-shares-residual/README.md) is ever used, that class votes as a class with a ceiling (default: at most 5% of the votes present) and has no vote on the reserved matters in §5.1. The WVV allows a departure from one-share-one-vote as long as at least one share keeps one vote; counsel confirms the article and the ceiling clause for that case only.

### 4.2 A vote-only share at par carries no value

The share pays no dividend and is returned at €1 on withdrawal and at liquidation. Buying it at €1 is not a benefit for the work: the member pays the CV, not the other way round. The count-tracks-hours fact that the [cheap-share dead-end](../../dead-ends/cheap-share-route.md) rejected is about **profit** shares. It does not apply to a share that cannot pay. The leonine rule (art. 4:2 WVV) still needs every share to take part in profit **or** in the liquidation balance; the €1 back is that part. Counsel confirms it is enough.

### 4.3 The yearly rebalance uses CV-native tools

- **More shares to a member, or a new member:** no statute change; the body named in the statutes decides within the entitlement rule (§1.2).
- **Fewer shares:** partial withdrawal at the *scheidingsaandeel* (art. 6:120 WVV), written as an automatic rule at the cut-off date. The repo already uses the neighbouring mechanism (*uittreding van rechtswege* on loss of a statutory *hoedanigheid*, arts. 6:121–6:122) on the cash-shares path.
- **Timing:** the WVV default lets members withdraw only in the first six months of the financial year. The cut-off date must fit that window or the statutes must set another rule (counsel).
- **Distribution tests:** the net-asset and liquidity tests apply to paying out the *scheidingsaandeel*. The amounts are tens of euros, and payment waits if a test fails.
- **One class only.** All governance shares have identical rights. Only the **count** per member moves. A right keyed to issue year would create one class per vintage by operation of law ([2026-09-11 §5](../../../docs/log/2026-09-11_cheap-share-ab-classes-sunset.md)); this design has none.

### 4.4 Majorities and quorum stay the WVV default

Because votes sit on shares, the statutory thresholds (a special majority for a statute change, the quorum rules) apply as written. No formula vote, no register with evidentiary status, no notary question about "who had how many votes". The only clauses counsel drafts are: the entitlement formula and who issues within it; the automatic partial withdrawal; the vote cap; the cut-off date.

### 4.5 The register decides entitlements — and it also feeds the fee

The accepted-hours register now decides two things: the option-2 weights `p` and the share entitlement `N_i`. Whoever accepts hours controls both. Attack vectors: inflating your own hours; a group accepting each other's hours; rejecting a rival's hours; farming shares with low-value hours on padded tasks. Rules that hold with the hours approach:

- nobody accepts their own hours;
- acceptance by consent inside the project circle, against an accepted task;
- the register is published to members, with an objection window before the cut-off;
- a yearly ceiling on hours that count for `V` (default 1,800);
- sample audits by the guardian circle (§5.1).

**Open (to be done):** a governance-distribution rule that does not rest on hours. The alternative "the governors distribute governance" has the dilemma the user named: people with many votes elect themselves and give themselves weight, or, if you may not vote for yourself, a hostile group excludes good stewards. Start with hours; return to this. The Cred idea on the [scoped-royalty path](../scoped-royalty-cred-q/README.md) has the same self-dealing surface.

---

## 5. Steward-ownership pieces

Steward-ownership has two halves. **Profits serve the purpose:** capital gets a capped return and the residual stays with the mission. The fee, the bond and the two-leg waterfall already give that half ([bond path §4.2](../capped-participating-bond/README.md)). **Control stays with the people who do the work** and cannot be sold or inherited. That half is this section.

### 5.1 Veto share

One share of a separate class G, held by a legal person that is not an investor and not a contributor: a private foundation (*stichting*) or a non-profit association (VZW). It pays no dividend and gets €1 at liquidation. Its approval is required for:

- a change to the mission (*doel* / *voorwerp*);
- a change to the rule that votes never attach to the fee, the bond, or any financial instrument;
- the entitlement formula, `δ`, the divisor, `k` and the cap floor;
- the asset lock and the mission lock (§5.2);
- sale, merger, conversion into another form, or dissolution;
- issuing any financial share class;
- the class G share's own terms — this one is automatic, because changing the rights of a class needs that class's consent.

The holder of the class G share acts through a **guardian circle** (see [docs/governance.md](../../../docs/governance.md)). Until the foundation exists, who holds the share is an open question (§8).

### 5.2 Asset lock and mission lock

An **asset lock** is a set of statutory rules that say the company's net assets can never flow to members beyond what they paid in:

- no dividend on the governance share; the *scheidingsaandeel* is fixed at the paid-in €1;
- no capital reduction to members;
- on liquidation the surplus goes to a named entity with a similar purpose, or, if that entity no longer exists, to one the GA chooses among entities with a similar purpose;
- proceeds of selling assets or intellectual property stay inside the lock;
- a **lock on the lock**: changing these clauses needs the veto share and a special majority.

A **mission lock** says what the company is for: the *doel* in the statutes plus "the designs stay open under CERN-OHL".

Why both matter here:

- They make "no liquidation rights" coherent and not leonine: every share gets €1 back, nobody gets the residual, the mission does.
- They remove the reason to sell or wind up the company to cash out.
- They protect the fee and the bond in the same way: both are capped, and nobody who controls the GA in fifteen years can capture the residual.
- They are the non-tax reason for the whole structure (art. 344 §1 WIB 92; DVB **(q)** and **(t)**): a lock that would still be there if every tax outcome were reversed.
- Without recognition as a social enterprise there is no legal cap forced on the company. The lock is purely statutory, so its strength is its entrenchment. That is what the veto share is for. Recognition as *sociale onderneming* is **not** sought ([ADR 2026-09-15](../../../docs/decisions/2026-09-15_votes-off-the-reward.md)).

### 5.3 Exit

A member who leaves has all governance shares withdrawn at €1 each and `V_i` set to zero. Leaving as a member does not touch an option-2 row or a bond position; each of those follows its own table.

---

## 6. Pair check against the fee and the bond

The rule from [mistake 2026-09-14](../../../docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md): list the facts the other instruments rely on being absent, and check that this one does not supply them.

| The other leg relies on | Does this leg supply it? |
| --- | --- |
| No euro price per hour of work (option 2) | **No.** The statutes state €1 per share and the entitlement formula. Money flows from the member to the CV, so it cannot be consideration for work. No document restates it as euros per hour or per `c`. |
| No unit conversion rate on `p` (option 2) | **No.** `V` and `N` are computed from accepted hours, never from `p`, and never in euros. |
| No principal on the contributor leg (option 2 §5.2) | **No.** The €1 per share is paid-in capital returned at par, not a loan and not an accrual base. |
| What a person may advance is never a function of hours (bond §8) | **No.** The bond stays cash-only and uncorrelated. |
| Lenders have no GA vote (bond §5.4) | **Kept.** Only governance shares vote; the class G holder is neither a lender nor a contributor. |
| Membership is not the allocation key of the fee (option 2 §6) | **Kept.** Share count never enters `P_t` or `p`. |

Implied number to compute before shipping: a member at 1,000 hours a year in steady state pays €20 for 20 shares. That is a membership fee scale, not a labour price.

---

## 7. What stays dead, and what was withdrawn on this path

| Sketch | Why not |
| --- | --- |
| A share with profit rights whose number tracks hours | The [cheap-share dead-end](../../dead-ends/cheap-share-route.md), unchanged |
| Voting rights keyed to the issue year of a share | One class per vintage by operation of law |
| Square root per (member, proposal) — QF or QV | Cross term and spreading bonus (§3) |
| Votes weighted by a register formula, one share per member | Withdrawn as unnecessary: it needs a statutory weighting formula, a register with legal status, and quorum work. Share count gives the same compression at the WVV default |
| Selling shares back each year to rebalance | Replaced by automatic partial withdrawal at the cut-off |
| A non-voting financial class | Not available in a CV (art. 6:19); investors are on the bond |

---

## 8. Open questions

- Counsel: the entitlement clause and which body issues within it; the automatic partial withdrawal clause and the six-month window; the vote-cap clause; the leonine minimum on a vote-only share; the class G share and the reserved-matters clause; the asset-lock and liquidation-destination clauses without social-enterprise recognition.
- Who holds the class G share until a foundation exists.
- Whether `δ = 0.25` and `k = 2` are the right start values (the tables in §2 are the tool for that discussion).
- **To be done:** a governance-distribution rule that does not rest on hours (§4.5).
- **To be done:** circles beyond the first one, domain descriptions, double links; admission, exit and exclusion; mediation; review dates and role terms; spend thresholds; a decision log — tracked in [docs/governance.md](../../../docs/governance.md).
