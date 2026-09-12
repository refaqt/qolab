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
