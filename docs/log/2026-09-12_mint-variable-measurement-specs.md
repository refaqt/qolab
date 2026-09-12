# 2026-09-12 — How each mint variable is measured, per role, and what it costs to run

**Role(s):** finance, business-dev

Third pass on the second mint variable. Passes one and two listed candidates ([2026-09-12 candidates](2026-09-12_second-mint-variable-candidates.md)); this one defines each as a rule a script can evaluate, says who types what and when, and prices the administration. Two constraints added by this pass: **every variable must be evaluable for every role**, and **no variable may add meaningful work** (no review rounds, no negotiation, no scoring meetings).

## The rule that makes the overhead disappear

The cost of a variable is not its formula. It is **who has to type something, and whether they want to**.

> **Every field is bonus-triggering, never penalty-triggering.** A field whose absence costs the person will be hidden or forgotten; a field whose presence earns something gets filled by the person who benefits. An unfilled field then means `m = 1.0`, not a dispute.

This inverts two rules from the earlier passes. “Self-accepted mints `0.8`” becomes “accepted by another person mints `+0.1`”; “missed external deadline mints `0.9`” becomes “met a recorded external deadline mints `+0.1`”. Same ordering of outcomes, opposite incentive on the paperwork. Nobody has to police a form.

Second consequence: prefer variables **computed from data recorded for another reason** over variables needing a new declaration. A variable whose input can be forgotten produces silent zeros, and then the diligent form-filler out-mints the person doing the work — which is the exact unfairness the multiplier is supposed to remove.

## The accept record

Everything below is a query over one record. Fields marked ★ are new; the rest exist already or are timestamps the board tool writes by itself.

| Field | Who fills it | When | Effort |
| --- | --- | --- | --- |
| `hours` | contributor | at accept | already |
| `accepted_by` | whoever accepts | at accept | already |
| `tier` | whoever posts the task | at posting | dropdown, 1 s |
| `posted_at`, `claimed_at`, `accepted_at` | tool | automatic | none |
| ★ `task_type` | whoever posts the task | at posting | dropdown, 2 s |
| ★ `due` + `due_source` | contributor | only if an outside party set a date | date + dropdown, 5 s |
| ★ `counterparty_ref` | contributor | only if an outsider signed something | paste a reference, 5 s |
| ★ `public_ref` | contributor | only if a public record exists | paste a DOI/URL, 5 s |
| ★ `closes` | contributor | only if it closes a listed open question | pick from the open list, 3 s |
| ★ `eliminates` | contributor | only if it kills a recurring task | dropdown, 3 s |
| `cites` (prevention rules) | contributor | already required by `.agents/rules/core.md` | already |

**Typical item: one dropdown.** The other five fields are the ones that pay, they are optional, and each is a copy-paste of something the person already has in hand (the letter with the deadline, the signed PDF, the DOI). No item needs all of them; most need none.

### The one real dependency: `task_type`

A flat list of maybe 40 types — `vat-filing`, `month-end-close`, `supplier-qualification`, `distributor-contract`, `grant-application`, `ce-dossier`, `cad-module`, `manual-chapter`, `warranty-claim`, `press-piece`, `trade-fair`, `test-protocol`. Maintained like the tier list: someone adds a type when a genuinely new kind of task is posted; roughly an hour a quarter. Variables 11, 12 and 13 all read it, and without it none of them work. It is the only structural addition in this pass.

Granularity rule, decided once: **the type is the kind of work, not the instance.** “Distributor contract” is one type; the second country is a *repeat*, not a new first-of-kind. That is deliberate — the second one is easier, and variable 12 pays whoever made it easier.

---

## Variable specs

Each card: what the variable is actually asking, the rule a script evaluates, what a human types, an instance for every role, and how it breaks.

### 11 · First-of-kind

**Asking:** has this organisation ever done this kind of thing before?

**Rule.** At accept, count accepted items with the same `task_type` and an earlier `accepted_at`. Count 0 → `+0.25`; count 1 → `+0.10`; else `0`.

**Typed by a human:** nothing beyond `task_type`. Fully computed.

| Role | An item that scores `+0.25` |
| --- | --- |
| Engineering / CAD | the first module released with a published parametric source |
| Purchasing | the first supplier put through a written qualification |
| Finance / admin | the first VAT-OSS registration |
| Legal / compliance | the first CE technical file assembled |
| Sales / distribution | the first distributor contract, any country |
| Marketing / community | the first trade fair the company exhibits at |
| Support / warranty | the first warranty claim run end to end under the new policy |

**Breaks when:** the type list is too fine — then every item is a first. This is why the list is short, flat, and maintained by one owner. It also self-limits: the bonus disappears as the organisation matures, which is correct.

**Cost:** zero marginal.

### 12 · Recurrence elimination

**Asking:** did this work permanently remove recurring hours from the board?

**Rule.** An item may name `eliminates: T` for a standing type `T` with at least two quarters of history. Let `H_before` be the median quarterly hours on `T` over the prior four quarters and `H_after` the median over the two quarters following acceptance. Bonus `= min(0.5, 0.5 · (H_before − H_after) / H_before)`, floored at 0. Retro-minted after those two quarters, at the lot’s original position on the curve.

**Typed by a human:** one dropdown, and only by someone claiming the bonus.

| Role | An item that scores |
| --- | --- |
| Engineering / CAD | a jig that removes manual alignment from every build |
| Purchasing | a framework agreement that ends per-order quote chasing |
| Finance / admin | a bank feed that ends manual reconciliation |
| Legal / compliance | a contract template that ends per-deal review |
| Sales / distribution | a configurator that ends hand-built quotations |
| Marketing / community | an FAQ that ends a recurring class of inbound questions |
| Support / warranty | a diagnostic guide that ends the most common call type |

**Breaks when:** the hours on `T` fall for an unrelated reason (the product line was dropped). Bounded by the `0.5` cap; accept the noise rather than adding a review.

**Cost:** zero typing, but it needs two quarters of history per type before it can pay anything. This is the one variable worth waiting for rather than launching with.

**Why it matters most:** in an hours ledger, the person who automates their own job away mints *less*. Every other variable here adjusts fairness; this one fixes a defect.

### 13 · Handover happened

**Asking:** can someone else now do this without the person who did it first?

**Rule.** For the earliest accepted item of type `T` by person A: if within 12 months an accepted item of type `T` exists by person B ≠ A, and A logged no hours on B’s item, then A’s item gets `+0.20`. Once per type per person.

**Typed by a human:** nothing. It is two rows in the ledger.

| Role | The substitution event |
| --- | --- |
| Engineering / CAD | someone else builds the module from the published files |
| Purchasing | someone else runs the qualification checklist on a new supplier |
| Finance / admin | someone else does the month-end close |
| Legal / compliance | someone else files the annual return |
| Sales / distribution | someone else runs the demo call from the script |
| Marketing / community | someone else publishes the newsletter |
| Support / warranty | someone else processes the RMA |

**Breaks when:** the type genuinely never recurs — then nobody is penalised, there is simply no bonus. Note it stacks with 11 on the same item (first to do it, and made it repeatable); the `[0.8, 2.0]` clip absorbs that, and the two facts are genuinely different.

**Cost:** zero. This is documentation quality measured **by the event of substitution**, so no document is ever read and rated.

### 14 · Unblocking others

**Asking:** was someone else waiting on this?

**Rule.** `+0.10` per distinct other person whose `blocked_by` item released when this was accepted, capped `+0.30`.

**Typed by a human:** the *blocked* person ticks a box on their own item — the only field in the whole set filled by someone other than the beneficiary.

| Role | Typical release |
| --- | --- |
| Engineering / CAD | a tolerance decision that releases the assembly drawing |
| Purchasing | a part number that releases the BOM freeze |
| Finance / admin | a budget line that releases a hire |
| Legal / compliance | a signed NDA that releases a supplier visit |
| Sales / distribution | a price list that releases distributor quoting |
| Marketing / community | approved photography that releases the launch page |
| Support / warranty | a spare-parts policy that releases claim handling |

**Breaks when:** people forget to declare the dependency — and they will, because the person typing is not the person paid. Silent zeros, exactly the failure the framing rule warns about.

**Verdict under the no-extra-work constraint: demote.** Keep the `blocked_by` field if the board wants it for planning, but do not mint on it until the data proves reliable.

### 15 · External commitment met

**Asking:** did an outside party set a date, and did we hit it?

**Rule.** If `due` is set with `due_source ∈ {authority, customer, funder, supplier, standards-body}` and `accepted_at ≤ due` → `+0.10`. Otherwise nothing. No penalty.

**Typed by a human:** a date and a dropdown, copied from the letter or mail that created the task in the first place.

| Role | Whose clock |
| --- | --- |
| Engineering / CAD | a certification body’s response window |
| Purchasing | a supplier’s quote validity date |
| Finance / admin | a VAT or annual-accounts filing deadline |
| Legal / compliance | a regulator’s request for information |
| Sales / distribution | a tender submission date |
| Marketing / community | a fair’s stand-material deadline |
| Support / warranty | a statutory warranty response window |

**Breaks when:** internal deadlines creep in. Only outside-set dates count — this is the whole reason the variable cannot be sandbagged, unlike the estimate-versus-actual version from the first pass, which is hereby dropped.

**Cost:** 5 seconds, on the minority of items that have an external date.

### 16 · Counterparty-confirmed

**Asking:** did somebody outside the company put their name on the result?

**Rule.** `+0.20` if `counterparty_ref` points to a document issued or signed by an outside party. Capped at one bonus per counterparty per quarter per person.

**Typed by a human:** paste a reference to a document you already received.

| Role | The confirming document |
| --- | --- |
| Engineering / CAD | a test house report or certificate |
| Purchasing | a countersigned supply agreement |
| Finance / admin | a filing receipt or an accountant’s sign-off |
| Legal / compliance | a granted registration |
| Sales / distribution | a signed order or distribution contract |
| Marketing / community | a third-party publication that ran the piece |
| Support / warranty | a customer’s accepted-resolution confirmation |

**Count, never amount.** No euro figure enters — a signature is a signature. Consequence to accept deliberately: ten small contracts out-mint one large one. The euro size of the deal already reaches the company through revenue, and `f` already bounds the person; putting deal value in the mint would price a point in euros and break the core constraint.

**Breaks when:** one agreement is split into several documents. The per-counterparty-per-quarter cap handles it.

**Cost:** 5 seconds, on items that produce a signature.

### 17 · Open question closed

**Asking:** did this finish something that was written down as open?

**Rule.** `+0.20` if `closes` names a question that appeared on the open list **before** the item was accepted, and a decision entry now records it as closed.

**Typed by a human:** pick from the open list — which the person closing a question wants to do anyway.

| Role | A listed question it might close |
| --- | --- |
| Engineering / CAD | which fastener standard the platform commits to |
| Purchasing | single-source versus dual-source for the drive |
| Finance / admin | the values of `k` and `r` |
| Legal / compliance | a DVB letter answered |
| Sales / distribution | direct sales versus distributors for a market |
| Marketing / community | which licence the documentation ships under |
| Support / warranty | who carries return shipping |

**Breaks when:** questions are invented in order to close them. The pre-existence requirement is the whole defence: the question must predate the work.

**Cost:** near zero — `docs/log/` and `docs/decisions/` already carry the open lists.

### 18 · Prevention rule cited

**Asking:** did a documented failure stop somebody else from repeating it?

**Rule.** A `docs/mistakes/` entry gets `+0.20`, once, the first time a later accepted item **by another person** lists it in the “prevention rules applied” line.

**Typed by a human:** nothing new — `.agents/rules/core.md` already requires every agent and contributor to state which prevention rules apply, and the log entries already do it.

| Role | A prevention rule that gets cited |
| --- | --- |
| Engineering / CAD | a tolerance stack that caused a scrapped batch |
| Purchasing | a supplier who missed lead time twice |
| Finance / admin | a euro spot price on a growing pool |
| Legal / compliance | *inbreng in nijverheid* needs a plan-ahead commitment |
| Sales / distribution | an exclusivity clause granted without a volume floor |
| Marketing / community | a launch announced before stock existed |
| Support / warranty | a policy promise that could not be met |

**Breaks when:** entries are farmed for volume. The bonus is once per entry, and it requires *another person* to have found it useful.

**Cost:** zero. It is the repair for the survival-in-service idea from the first pass, which punished exploration: here a well-documented dead end mints.

### 19 · Durable public record

**Asking:** does something citable exist outside our own systems?

**Rule.** `+0.20` if `public_ref` resolves to a durable, third-party-hosted record: a DOI, a registry entry, a published standard, an archived article. Not a post that can be edited or deleted.

**Typed by a human:** paste the identifier you were given.

| Role | The record |
| --- | --- |
| Engineering / CAD | a defensive publication of a design, with a DOI |
| Purchasing | a published qualified-supplier list |
| Finance / admin | filed annual accounts in the public register |
| Legal / compliance | a registered licence or trademark entry |
| Sales / distribution | a published price list or public tender award |
| Marketing / community | an archived article or conference talk |
| Support / warranty | the published warranty policy version |

**Why it earns its place here:** under a copyleft strategy, publishing *is* the IP defence — a steady defensive-publication cadence creates prior art and protects freedom to operate without a patent budget. This makes the cheapest available protection somebody’s personal interest.

**Breaks when:** it pushes premature publication of something still commercially sensitive. Publication timing stays a board call; the multiplier follows the decision, it does not force it.

**Cost:** 5 seconds, on items that produce a public record.

### 20 · Accepted by another person

**Asking:** did anyone other than the author sign this off?

**Rule.** `+0.10` if `accepted_by ≠ contributor`.

**Open point that decides its fate:** if the design already requires every item to be accepted by the board or a parent project — which the current spec reads as — then this field is constant, has no variance, and mints nothing anywhere. **Then drop it.** It is worth keeping only if self-accept is genuinely common, and it must never become a reason to hold review meetings.

---

## What it costs to run

| # | Variable | New typing | By whom | Computed | Forget-rate risk |
| --- | --- | --- | --- | --- | --- |
| 11 | First-of-kind | none | — | yes | none |
| 13 | Handover | none | — | yes | none |
| 18 | Prevention cited | none (already required) | contributor | yes | none |
| 12 | Recurrence elimination | 1 dropdown | beneficiary | yes | low |
| 15 | External commitment | date + dropdown | beneficiary | yes | low |
| 16 | Counterparty-confirmed | 1 reference | beneficiary | yes | low |
| 17 | Question closed | 1 pick | beneficiary | yes | low |
| 19 | Public record | 1 reference | beneficiary | yes | low |
| 20 | Accepted by another | none | — | yes | none (may be constant) |
| 14 | Unblocking | 1 tick | **someone else** | yes | **high** |

Every row except 14 is filled by the person who gains from it. Nothing on this list requires a reviewer to read the work, a meeting, or a negotiation. The board's only recurring duty is the one it already has: post tasks with a tier, and keep the type list tidy.

## Live formula

```
m = tier · ( 1
    + 0.25 first_of_kind | 0.10 second        # 11  computed
    + 0.20 handover                           # 13  computed
    + 0.10 external_commitment_met            # 15  one date
    + 0.20 counterparty_confirmed             # 16  one reference
    + 0.20 question_closed                    # 17  one pick
    + 0.20 prevention_cited                   # 18  computed, retro
    + 0.20 public_record                      # 19  one reference
    + ≤0.50 recurrence_eliminated )           # 12  retro, needs history
  clipped to [0.8, 2.0]

c = hours × 100 × m        f = hours × frozen band     (unchanged)
```

`tier` is the pre-declared need tier with neglect escalation (`1.0 / 1.25 / 1.5`, `+0.1` per unclaimed month, cap `+0.5`) from the first pass. The clip is what stops a single item collecting five bonuses into a 2.5× outlier.

## Worked quarter

One accepted item per role, hours held equal at 40 so only `m` moves.

| Role | Item | Bonuses | `m` | `c` |
| --- | --- | --- | --- | --- |
| Finance | First VAT-OSS registration, filed on the authority’s date | 11 first, 15 on time, 16 receipt | 1.55 | 6 200 |
| Support | Diagnostic guide; call volume on that type halves | 12 (retro, −50 %) | 1.25 | 5 000 |
| Sales | Second distributor contract, signed | 16 signature | 1.20 | 4 800 |
| Legal | CE technical file, first one, registration granted | 11 first, 16 granted, 19 registry | 1.65 | 6 600 |
| Purchasing | Supplier qualification; a colleague later runs the checklist | 13 handover | 1.20 | 4 800 |
| Marketing | Newsletter, third issue, no external date | none | 1.00 | 4 000 |
| Engineering | Module released and defensively published with a DOI | 19 record | 1.20 | 4 800 |

Spread 1.00–1.65 on identical hours. Two observations worth carrying into the decision: the routine repeat item sits at `1.00` by design and is not punished, and no row here is unreachable by any other role — the finance row's shape (first-of-kind, external date, receipt) is exactly the shape of a first tender submission or a first certification.

## Decisions

Proposed (not accepted, no ADR): the framing rule — **bonus-triggering fields only, no penalties** — plus the accept record above. `f`, `p = c0 · c^k`, and the `alloc / rem` burn are untouched throughout; `m` moves share of `P_t` only.

Recommended live set, in order of what it costs to start:

1. **From day one, no new work:** 11, 13, 18 (and 20 only if self-accept turns out to be common). All computed; the only prerequisite is `task_type`.
2. **From day one, one optional field each:** 15, 16, 17, 19.
3. **After two quarters of history:** 12 — the highest-value variable and the only one that needs a baseline.
4. **Not minted for now:** 14, and every hardware-bound candidate from the first pass (4–8), which become optional rows inside a role’s tier definition rather than global factors.

Dropped outright: estimate-versus-actual reliability (sandbaggable), participation floors (penalises part-timers), and anything euro-denominated.

## Open Questions

- Is `accepted_by ≠ contributor` already constant under the current design? If yes, 20 is dead weight — settle this before building anything.
- Who owns `task_type`, and does editing the list retro-mint? Working answer: one owner, no retro-mint on taxonomy edits.
- 12 pays the eliminator, but the person who used to do that recurring work loses future `c`. Is the `0.5` cap the whole answer? A share of the saved hours would be closer to a euro claim — check against the no-euro constraint before proposing it.
- Cap interaction: several bonuses are retro-minted (12, 18, and 13 in effect). Confirm each retro-mint lands at the lot’s original curve position and keeps the lot’s vintage, or the concave curve silently shrinks them.
- Per-role reachability: run a real past quarter and compare achievable `m` distributions per role. If one role structurally tops out lower, the variable is a role bonus wearing a fairness costume.
- **(r)** for DVB stands, with 16 as the worked example — “a counterparty signed” is the closest thing in the set to pay-for-performance optics, and pay-for-performance is a wage story under **(c)**.

## Next Steps

- Settle the 20 question and the `task_type` ownership; both are cheap and both block the rest.
- Build nothing yet. Take one past quarter across all roles, hand-compute `m` under the live formula, and look at the per-role spread before any of this reaches the option-2 spec.
- Keep the field list closed at what is above. Every further field is a tax on every future item.
