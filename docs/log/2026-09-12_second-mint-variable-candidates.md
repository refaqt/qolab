# 2026-09-12 — A second variable in the mint besides contribution

**Role(s):** finance, business-dev

## What happened

Asked whether the weights `p` can depend on something besides contribution — a quality-like variable — **without** judging every contribution, and with a variable that is objective, fair, and works for **all** roles (engineering, cad, software, finance, purchasing, business-dev, marketing). Context: a startup around **open-source machines**, so diffusion of the design is part of what the company is for. Ten candidates below, with the constraints any of them must survive.

### Where it would sit

Today there is **one degree of freedom per accepted item: hours** ([2026-09-09](2026-09-09_hours-cap-and-project-contractor.md)).

| Ledger | Today | With a second variable |
| --- | --- | --- |
| Contribution points `c` | `hours × 100` | `hours × 100 × m` |
| Documented effort `f` | `hours × frozen band` | **unchanged** |

`m` is a dimensionless, bounded multiplier on the **points** ledger only; `p = c0 · c^k` and the burn `p_i · (alloc_i / rem_i)` are untouched. Leaving `f` alone is what keeps this out of the euro path: the invoice ceiling per person stays `k · Σ hours × band`, so `m` moves **share of `P_t`**, never the size of the cap. A multiplier on `f` would instead be a second rate card, i.e. quality priced in euros per hour.

### Constraints a candidate must survive

1. **No euro inside `m`.** No “this task is worth €5 000”, no bounty in euros, no per-person revenue attribution. Any euro in the multiplier re-imports `€/point` and therefore `€/p` — [unit price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md), [ADR 2026-09-04](../decisions/2026-09-04_fee-cap-not-unit-price.md).
2. **No per-item judgment call.** `m` comes from a machine-checkable fact, a tier declared **before** the work is claimed, or a countable external event. A committee scoring merit is what we are avoiding, and it is also the least fair thing in the list.
3. **Role-neutral by construction.** Define `m` on the *task or artifact*, never on the discipline or the person. A rule that only has meaning for code fails.
4. **Bounded and non-compounding.** `m ∈ [0.8, 2.0]` on the product of all active factors, per lot. `p = c0 · c^k` is concave, so a large `m` on a big early lot moves everything; unbounded stacking of three factors is a 4–8× swing in weight.
5. **No clock that keeps running after payout.** `m` must not be a function of how long a lot stayed unpaid — that is the trailing coupon / gold rush again ([2026-09-03](../mistakes/2026-09-03_immediate-multiple-gold-rush.md)). Calendar age of the *artifact in service* (candidate 7) is a different fact from calendar age of an *unpaid balance*.
6. **Late-arriving `m` retro-mints at the lot’s own curve position.** Candidates 6–8 are only knowable months later. Minting the bonus at today’s cumulative `c` silently shrinks it (concave curve), and it would carry today’s vintage. Recompute that lot’s `Δp` with `m` at the `c` it faced, keep vintage `Y+1` of the original work.
7. **Dispersion is a transfer, not new money.** `Σ p` grows, so a higher `m` for one person dilutes everyone else’s share of `P_t`. That is the point, but it means `m` needs to be published as a rule up front, not tuned per round.

## Ten candidates

Ordered roughly by cost to run.

### 1. Pre-declared need tier on the task

Board/GA marks each posted task with an ordinal tier (`1.0 / 1.25 / 1.5`) tied to the roadmap **before** anyone claims it. Judgment is about the *need*, never the output or the person, and the same tier applies to whoever picks it up.

- Objective enough: pre-committed, public, identical for all takers.
- All roles: the board covers supplier qualification, a doc rewrite, a CAD module, a grant application.
- Watch: set the tier from roadmap position, **not** from a euro value of the task, or constraint 1 breaks. Freeze the tier at claim so it cannot be renegotiated afterwards.

### 2. Neglect escalation (unclaimed-time bump)

A task that sits unclaimed on the board escalates automatically: `+0.1` per full month, capped at `+0.5`. Pure clock arithmetic, zero human input, and it prices exactly the thing a startup struggles with — nobody wants the boring job.

- Objective: a timestamp difference.
- All roles: strongest for the unglamorous work in every discipline (test rigs, VAT filings, RMA handling, tolerance documentation).
- Watch: collusive waiting (everyone leaves it to ripen). Mitigate with the cap and by escalating only tasks the board has marked as *required this quarter*.

### 3. Peer-verified vs self-accepted

Binary: an item accepted by someone other than the author mints at `1.0`; a self-accepted item mints at `0.8`. This is not a quality score — the accept event already exists in the ledger; it only distinguishes *reviewed* from *unreviewed*.

- Objective: who clicked accept.
- All roles: review = a second signature on a supplier contract, a rebuilt part from the published files, a reread of the ruling annex.
- Watch: pay the reviewer’s hours as normal work, or review will not happen. Reciprocal rubber-stamping is the failure mode; rotate reviewers, and do not let a pair review only each other.

### 4. Reproducibility gate (machine-checked)

The deliverable passes the automated check for its artifact type — for machine work `python doqs/scripts/validate_all.py` (OKH metadata, BOM, source files not only exported STLs, licence headers, build instructions, CI green). Fails → `0.8`, passes → `1.0`.

- Objective: a script exit code. No human judges anything.
- All roles: each role declares its checklist once (purchasing → signed contract and datasheet in the repo; finance → reconciled entry with source document; marketing → asset with source file and licence). Per-role checklists, one shared rule.
- Watch: this is the closest thing to “quality” that can be had for free, and for open hardware it is the quality that matters — a design nobody can rebuild is not an open design. Keep the checklist mechanical; the moment a line reads “is well written”, it is a judgment.

### 5. Structural depth of the artifact

Position in the declared module tree: work on something many other modules depend on (shared frame, core library, the rate card, the compliance pack) mints above leaf work. Read from the dependency graph *as declared at accept time*, so it is known immediately.

- Objective: graph position, not opinion.
- All roles: “many things depend on this” exists for a contract template and a jig as much as for a library.
- Watch: incentive to declare spurious dependencies. Depth must be a property of the module tree the project maintains anyway, and changing the tree must not retro-mint.

### 6. Realized downstream reuse

Later **accepted** items cite the artifacts they build on. Reuse by a *different* author, counted over a bounded window (say 18 months), gives up to `+0.5`.

- Objective: a count in the ledger, like citations.
- All roles: a reused supplier qualification, a reused test protocol, a reused module, a reused funding dossier.
- Watch: self-citation (require distinct authors), rich-get-richer on old core modules (decay the window), and lag — this one arrives as a retro-mint under constraint 6.

### 7. Survival in service

The artifact is still in the shipped configuration at T+12 months → `+0.2`; replaced or reverted inside 3 months → no bonus (never a penalty below `1.0`).

- Objective: state of the release at a date.
- All roles: a supplier still supplying, a doc still current, a fixture still on the bench.
- Watch: this punishes exploration, and this repo *values* dead ends — see `docs/mistakes/` and the four dead-end routes in `architecture.md`. Exempt items the board accepted as an explicit spike/investigation at accept time. That exemption is a task-type flag, not a verdict on the result.

### 8. External replication of the module (open-source-specific)

Countable third-party adoption of the module: independent builds registered, forks with substantive changes, OKH package pulls, issues opened by non-members. Attributed to the **module**, then split across its contributors by their hours in it — never to a person directly. Up to `+0.5`, retro-minted.

- Objective: external events nobody inside can conjure.
- All roles: whoever made the module buildable — the CAD, the BOM, the manual, the video, the supplier list — shares in it.
- Watch: this is the one variable that points at the actual mission (diffusion of an open machine) rather than at internal process, and the one most worth the plumbing. Vanity metrics (stars, downloads of a PDF) are gameable; registered builds and non-member issues are much less so. Module-level attribution avoids ranking people.

### 9. Commitment reliability

Per period, compare accepted-and-delivered hours against hours committed at accept: deliver in the window → `1.0`; miss without renegotiating before the deadline → `0.9` on that lot only.

- Objective: two timestamps and two numbers already in the ledger.
- All roles: a commitment is a commitment.
- Watch: it rewards sandbagging estimates unless renegotiation-before-deadline is free (it should be — the point is the signal, not the punishment). Keep it symmetric-free: no bonus for beating the estimate, or estimates inflate. This is the candidate closest to judging behaviour; it is in the list because a startup dies of missed commitments, not of imperfect work.

### 10. Sustained participation floor

A step, not a race: a lot minted in a quarter where the contributor cleared a low floor (e.g. 20 accepted hours) mints at `1.0`; below the floor, `0.9`. Rewards showing up continuously rather than in bursts.

- Objective: calendar arithmetic.
- All roles: identical rule for everyone.
- Watch: **fairness caveat — the weakest of the ten.** It disadvantages people with caring duties, a day job, or a seasonal role, and it correlates with availability rather than with anything the project needs. If continuity is genuinely the goal, the honest instrument is the *role* commitment in hours/week that already exists, not a mint penalty on part-timers. Listed for completeness; recommend against.

## Rejected on sight

- **Euro-denominated bounties** on tasks — states `€/point` directly (constraint 1).
- **A contributor election trading cap for weight** (“take less `f`, get more `p`”) — an exchange rate between euros and `p` by construction; the cleanest violation of [ADR 2026-09-04](../decisions/2026-09-04_fee-cap-not-unit-price.md) in the list, and superficially the most attractive.
- **Seniority / band on the points ledger** — the frozen band belongs to `f` only; on `c` it is a market wage entering the mint ([2026-09-04](2026-09-04_points-per-hour-weight.md)).
- **Per-person revenue attribution** — a euro number per contributor, and unattributable for machines anyway.
- **Retroactive merit scoring by a committee** — the thing the question rules out, and the least fair.
- **Any `m` that grows with how long a lot stayed unpaid** — trailing coupon ([2026-09-03](../mistakes/2026-09-03_immediate-multiple-gold-rush.md)); illiquidity already lives in the opened cap, and the freeze after 1× is what bounds it.

## Decisions

Proposed (not accepted, no ADR): if a second variable is added, it enters as a bounded dimensionless `m` on `c` only, leaving `f`, `p = c0 · c^k`, and the `alloc / rem` burn untouched.

Recommended shortlist — three factors that compose and cover ex-ante need, mechanical quality, and realized impact:

```
m = tier(task) × gate(artifact) × (1 + reuse_bonus)     clipped to [0.8, 2.0]
      cand. 1+2      cand. 4              cand. 6/8
```

- **Now (cheap, no new plumbing):** 4 (validator gate) and 3 (peer-verified), both binary, both already implied by the accept step.
- **Next (needs a board habit):** 1 + 2 — tier declared at posting, auto-escalation while unclaimed.
- **Later (needs a citation/adoption feed):** 6 and 8 as retro-mints. 8 is the one that ties weight to open-hardware diffusion, which is the company’s actual thesis.
- **Not recommended:** 10; 7 only with a spike exemption; 9 only if renegotiation before the deadline is free.

## Open Questions

- New DVB question **(r)**: does a non-euro, published multiplier on the points ledger change the mint characterisation under **(a)** / **(i)**? Working view: it is still hours renamed, since no euro enters `m` and `f` does not move — but a multiplier that visibly tracks “value delivered” is exactly what an inspector reads as pay-for-performance, and pay-for-performance is a wage story ((c)). Ask before the multiplier is in a contract annex, not after.
- Does `m` on `c` disturb the arm’s-length analysis? `f` is unchanged per person, so the euro exposure of the CV is unchanged; only the split of `P_t` moves. Confirm that the 10× discussion in [2026-09-10](2026-09-10_arms-length-10x-and-repo-review.md) is untouched.
- Interaction with the burn: two contributors with equal `f` but different `m` burn `p` at the same `alloc / rem` fraction, so the higher-`m` person exhausts their cap **sooner** in euros per unit of weight. Is that intended? It reads as “better work gets paid earlier”, which is defensible, but it should be a decision, not an artefact.
- Nested projects: does `m` apply to local `c_j` inside a sub-project, to the parent’s admitted points `A_{t,j}`, or to both? Applying it twice compounds silently (constraint 4).
- Who owns the tier list in candidate 1 — board or GA — and how is a tier change contested?
- Lot bookkeeping: `m` is per lot, so lots now carry a multiplier as well as a vintage and a band. Check this against “keep lots, not one blended personal cap”.

## Next Steps

- Pick the shortlist (or reject the whole idea) before writing any of it into the option-2 spec; nothing here is accepted.
- If candidates 4 and 3 are taken, write the per-role artifact checklist once and point `validate_all.py` at it; then an ADR.
- Draft **(r)** into [dvb-questions.md](../../token-system-design/dvb-questions.md) only once a multiplier is actually in the spec — the gate before launch is still **(a)–(d)**.
- Do not calibrate any `m` against a euro figure, at any point in the drafting.

## Second pass — ten variables that do not lean on hardware artifacts

The first ten skew engineering. Candidates **4, 5, 6, 8** (validator gate, module-tree depth, reuse citations, external replication) and partly **7** (survival in a release) are measured on a repo, a module tree, or a shipped configuration. A machine company is mostly *not* machine design: purchasing, finance and admin, legal and compliance, sales and distribution, marketing and community, support and warranty, grants and funding. A variable those roles cannot be scored on is a variable that quietly pays engineers more.

### The test that generalises

The first list drew its facts from the **artifact's technical substrate** (does it validate, is it depended on, is it still in the release). That substrate only exists for hardware and software. The role-general version draws facts from three sources every role has:

| Source of the fact | Why it is objective | Available to |
| --- | --- | --- |
| The ledger itself (hours, task types, precedence, blocking) | Already recorded for other reasons | Every role |
| A **different person** inside the org acting on the work | The event is someone else's behaviour, not a verdict | Every role |
| A **counterparty outside** the org (authority, customer, supplier, funder, registry) | Nobody inside can conjure it | Every role |

**Admission test for any future candidate:** if it cannot be evaluated for the bookkeeper doing the VAT return and for the person answering warranty mail, it does not go in the mint. Both of the tier candidates from the first pass (**1** need tier, **2** neglect escalation) pass it unchanged and stay the backbone; the ten below replace the artifact-bound ones.

### 11. First-of-kind vs repeat (precedent)

At accept, the ledger is queried for a prior accepted item of the same task type. No precedent → `1.25`; a repeat with a template in place → `1.0`.

- Fact: does a prior item of this type exist. A query, not an opinion.
- Roles: first distributor contract, first grant dossier, first CE file, first VAT-OSS registration, first trade fair, first warranty claim handled — as much as the first machine.
- Why it fits: it pays the risk of doing something nobody here has done, and it **decays on its own** as the org matures. It is also the honest version of “early work mints more” at task level, next to the curve’s version at org level.
- Watch: task-type granularity is the whole game. Too fine and everything is first-of-kind; the type list must be maintained like the tier list.

### 12. Recurrence elimination

An item that measurably removes recurring hours from the board: bonus scaled to hours removed per year against the recurring task’s prior median, capped `+0.5`.

- Fact: logged hours per period on that standing task, before and after.
- Roles: a payment integration that ends manual reconciliation; a contract template that ends per-deal legal review; an FAQ that ends a class of support mail; a supplier portal that ends chasing quotes; a fixture that ends manual alignment.
- Why it fits: the single most valuable and least visible work in a small company, invisible in an hours ledger because it *reduces* hours — the person who automates their job away currently mints less. This is the candidate that most directly corrects the hours rule.
- Watch: inflating the baseline by working slowly first. Use the median of prior periods, and require the recurring task to have existed as a board item before the fix.

### 13. Handover (substitution actually happened)

A different person later performed the same task type from the written record, in a window where the author logged no hours on it → `+0.2` to the original item.

- Fact: two rows in the ledger, different people, same task type.
- Roles: someone else runs the month-end close, sends the supplier RFQ, does the demo call, answers the standards questionnaire, rebuilds the module.
- Why it fits: it measures documentation quality **by the event of substitution**, so nobody reads and rates the document. It attacks bus-factor, which is what actually kills a small company.
- Watch: only for task types that recur; exempt genuinely one-off items rather than faking a handover.

### 14. Unblocking others

Items are logged with `blocked-by` where that is true. When the blocker is accepted, count the **distinct other people** whose items unblock: `+0.1` each, capped `+0.3`.

- Fact: an edge in the task board, declared by the *blocked* person, not by the author.
- Roles: legal unblocks sales; purchasing unblocks assembly; finance unblocks hiring; a translated manual unblocks a distributor.
- Why it fits: this is candidate 6 (downstream reuse) with the code-citation plumbing removed — the same “others build on this” signal, from a board every role already uses.
- Watch: the declaration must come from the blocked party, and self-blocking must not count.

### 15. External deadline met

For items whose deadline was set **outside** the org — authority, customer, funder, supplier, registry — delivered on time `1.0`, missed without renegotiating before the date `0.9`.

- Fact: two dates, one of which we do not control.
- Roles: filings, tender responses, grant deadlines, RMA windows, customer delivery dates, standards consultation replies.
- Why it fits: strictly better than the first pass’s commitment reliability (candidate 9), which could be gamed by sandbagging the estimate. You cannot sandbag the tax authority. Keep the internal-deadline version out for exactly that reason.
- Watch: apply only where the external date is documented at accept, or it becomes a self-set deadline again.

### 16. Counterparty-confirmed outcome

The item ends in an outsider putting their name on something: a signed contract, a supplier admitted to the qualified list, a submitted dossier acknowledged, an accreditation granted, an accepted delivery, a third-party publication. Binary `+0.2`.

- Fact: a countersignature or a receipt exists.
- Roles: the strongest coverage of any candidate — sales, purchasing, legal, finance, marketing, certification.
- **Count, never amount.** A deal is a deal; the euro value must not enter, or the mint carries a euro figure and constraint 1 breaks. Consequence to accept up front: ten small contracts out-mint one large one. That is the price of keeping euros out, and it is the right trade — the euro size of the deal already flows to the company, and `f` already bounds the person.
- Watch: splitting one agreement into several to farm the bonus; count per counterparty per period, not per document.

### 17. Open question closed

The item closes a question that was **already listed** in a prior log entry or ADR, and the closure is recorded in a new accepted decision → `+0.2`.

- Fact: the question was written down before the work started; a decision file now answers it.
- Roles: this repo’s open questions are tax, legal, and finance, not engineering. Look at `docs/log/*` — the open lists are DVB letters and contract wording.
- Why it fits: the org already runs on log / decisions / mistakes. Weighting closure pays the unglamorous act of *finishing* a question instead of opening three more.
- Watch: inventing questions in order to close them. Only questions logged before the item was accepted, and only closure by a decision the board accepts.

### 18. Prevention rule later cited

A `docs/mistakes/` entry earns `+0.2` when a **later accepted item by another person** cites its prevention rule. The mistake write-up itself mints as ordinary hours; the bonus is the citation.

- Fact: a citation count, distinct author, bounded window.
- Roles: the existing entries are a growing pool, a gold rush, a euro par, a revisor rule — finance and legal, all of them.
- Why it fits: it is the **repair** for the first pass’s survival-in-service candidate, which punished exploration. Here a dead end that saved the company from repeating it *mints*. In a startup, cheap failure documented well is worth more than a mediocre success.
- Watch: quantity of entries over usefulness — the citation requirement is what filters it; do not bonus the writing itself.

### 19. Durable public record

The item produces something citable and archived outside the org: a DOI'd defensive publication, a registry entry, a published standard or spec, a filed dossier that becomes public, an archived article. Binary `+0.2`.

- Fact: a resolvable identifier exists.
- Roles: marketing, legal/IP, engineering, community — anyone who put something in a public record.
- Why it fits: for a copyleft open-hardware company, publishing *is* the IP strategy — a defensive-publication cadence creates prior art and protects freedom to operate without a patent budget. Weighting it makes the cheapest IP defence someone's personal interest, and unlike candidate 8 it does not need adoption telemetry.
- Watch: vanity output. Require durable and citable (DOI, registry, archive), never a social post or a page that can be edited away.

### 20. Peer-verified vs self-accepted *(carried over unchanged)*

Candidate 3 from the first pass is already role-neutral and free: `1.0` reviewed by another person, `0.8` self-accepted. It stays, and it is the precondition for several of the above — 14, 16 and 17 all rely on someone other than the author having touched the record.

### Role coverage

| # | Variable | Eng | Purch | Fin/Admin | Legal | Sales | Mktg/Comm | Support |
| --- | --- | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 11 | First-of-kind | ● | ● | ● | ● | ● | ● | ● |
| 12 | Recurrence elimination | ● | ● | ● | ● | ● | ● | ● |
| 13 | Handover happened | ● | ● | ● | ● | ● | ● | ● |
| 14 | Unblocking others | ● | ● | ● | ● | ● | ● | ○ |
| 15 | External deadline met | ○ | ● | ● | ● | ● | ○ | ● |
| 16 | Counterparty-confirmed | ○ | ● | ● | ● | ● | ● | ● |
| 17 | Open question closed | ● | ● | ● | ● | ○ | ○ | ○ |
| 18 | Prevention rule cited | ● | ● | ● | ● | ● | ● | ● |
| 19 | Durable public record | ● | ○ | ○ | ● | ○ | ● | ○ |
| 20 | Peer-verified | ● | ● | ● | ● | ● | ● | ● |

● routinely applies ○ applies sometimes. Compare the first pass, where 4, 5, 6, 8 are ● only in the first column.

### Also rejected

- **Revenue, deal value, pipeline, margin, cost saved in euros** — the obvious sales and purchasing metrics, and all disqualified by constraint 1. A commission is a euro price on a point. Candidate 16 is the euro-free substitute.
- **Governance participation** (GA attendance, board seats) — the design keeps governance membership off the reward; paying weight for it merges the two instruments.
- **Response latency alone** — rewards a fast superficial reply over a slow correct one, and unlike 15 the clock is ours.
- **Headcount or budget managed** — seniority by another name, and it puts a euro figure in the mint.
- **Customer satisfaction scores** — a judgment, just outsourced, and only some roles face a customer.

### Revised shortlist

```
m = tier(task) × verified × (1 + first_of_kind + recurrence + external + citation)
      cand. 1+2   cand. 20      11        12        15/16      14/18
                                             clipped to [0.8, 2.0]
```

- **Now, free, no new plumbing:** 20 (peer-verified) and 11 (first-of-kind) — both are ledger queries at accept.
- **Next, one board convention each:** 15 (external deadline field), 14 (`blocked-by` declared by the blocked party), 16 (counterparty receipt attached).
- **Then, the two that pay for themselves:** 12 (recurrence elimination) and 18 (prevention rule cited).
- **Keep from the first pass only:** 1, 2, 3(=20). The hardware-bound 4–8 become *optional role-specific gates inside* the tier, not global factors — engineering’s artifact checklist is then one row of the same rule that gives purchasing “signed contract and datasheet filed”, not a separate advantage.

## Open Questions (second pass)

- Task-type taxonomy is now load-bearing for 11, 12 and 13. Who maintains it, and does changing it retro-mint? Working answer: no retro-mint on taxonomy edits.
- 12 measures hours *removed*. Removing hours also removes future `c` for whoever used to do that task. Is the `+0.5` cap enough compensation, or does the eliminator need a share of the saved hours for a bounded period? A share of saved hours is close to a euro claim — check it against constraint 1 before proposing it.
- 16 pays per counterparty event, so a role with many small counterparties (support) mints more often than one with few large ones (a distributor deal). Is per-period normalisation needed, and does that reintroduce a judgment?
- Roles with mostly ○ rows (marketing, support) rely more on 1, 2, 11, 12, 20. Verify with real board data that the achievable `m` distribution is comparable across roles — if marketing structurally tops out at 1.2 and engineering reaches 1.8, the variable is a role bonus wearing a fairness costume.
- Does 19 conflict with anything in the copyleft/defensive-publication cadence, i.e. could weight pressure cause premature publication of something still commercially sensitive? Publication timing should stay a board call, with the multiplier following it.
- **(r)** unchanged, and now sharper: 16 (“a counterparty signed”) is closer to pay-for-performance optics than anything in the first list. Same question to counsel, with 16 as the worked example.

**Measurement, per-role instances, and administration cost for each of these: [2026-09-12 measurement specs](2026-09-12_mint-variable-measurement-specs.md).** That pass adds two constraints (every variable evaluable for every role; no variable may add review or negotiation work), which demotes 14 and drops the estimate-versus-actual form of 9.

## Next Steps (second pass)

- Decide the shortlist against real board data, not in the abstract: take one past quarter across all roles, compute `m` under the revised formula, and look at the dispersion **per role** before anything is written into the option-2 spec.
- If the taxonomy is adopted, it belongs in the spec next to the two ledgers, not in a tool.
- Still no ADR. Nothing in either pass is accepted.
