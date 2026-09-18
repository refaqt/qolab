# 2026-09-17 — Burn `p` on ecological damage instead of on the effort cap (open)

**Role(s):** finance, business-dev

**Status:** Open sketch. Not accepted. No ADR. Not a new path folder. It would replace two accepted pieces of the live [option-2 spec](../../token-system-design/paths/option-2-contingent-fee/README.md): the ceiling built on documented effort (§5) and the burn of `p` against that ceiling (§6, [note](../../token-system-design/paths/option-2-contingent-fee/p-burn-remaining-cap.md)).

**Prevention rules applied:** [mission as a design constraint](../mission.md) — this sketch passes that test better than any earlier one; [do not put a euro price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [remaining `p` is not remaining euros](../mistakes/2026-09-04_cheap-share-euro-par.md); [paid-off `p` must not keep seniority on later work](../mistakes/2026-09-08_unburned-p-after-cap.md); [a second instrument must not publish the comparable](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).

## What happened

Recorded an idea about what should make the weights (`p`) shrink. Today the ceiling on what a contributor may invoice comes from documented effort, which is hours times a frozen rate band. That same ceiling drives the burn: taking part of your ceiling retires the same share of your weight. The idea drops both and uses a measure of ecological damage instead.

### The idea

- Stop using a ceiling based on rate times hours, and stop burning `p` against it.
- Measure the ecological destruction caused by making the products and by running the operations. Use a **relative** number.
- Multiply that number by a factor `k_eco` and by a number of contribution points.
- Put those points on the mint curve (`p = c0 · c^k`). That gives an amount of `p`.
- Burn that amount across **all** holders of `p`, each in proportion to their share of `p`.
- Regeneration works the same way in the other direction. Work that gives nature back **mints** `p` by the same route.
- Intended effect: making more profit then means doing regenerative business, and damaging nature costs the holders.
- `k_eco` is set by the general assembly of the stewards.
- The destruction number is produced by independent institutions, not by Refaqt.

### Working read (not a decision)

**1. A burn spread over everyone changes nothing in the same year.** The yearly pool is divided by each person's share of the total weight. If every weight is cut by the same share, every person's share of the total stays the same. Two holders at 60 and 40 weights, both cut by ten percent, become 54 and 36. That is still 60 and 40 percent. The same money leaves the company, to the same people, in the same amounts. So a proportional burn cannot make damage cost anything in the year it is measured.

**2. What the burn does change is the value of old work against new work.** New work mints a fixed amount of weight on the curve. If the old stock is cut, each new contribution counts for more in the next split. So the ecological number is really a **speed at which old weight fades**, not a brake on payout. Damage would make newcomers catch up faster with people who contributed earlier. That may be a useful lever. It is not the lever the idea is asking for.

**3. To make damage cost money, the number has to sit on the pool, not on the weights.** The yearly pool is the amount that leaves the company. It is already set each year by policy: a share of profit or EBITDA, a cash test, reserves, and money kept for the mission. An ecological factor there changes euros. The same factor on `p` only changes the order of the queue. If this idea is taken further, test `k_eco` on the pool first.

**4. The effort ceiling also does legal work, and nothing here replaces it.** The ceiling is the reason the payment can be defended as a normal business cost, and the reason we can say a ceiling is not something "to be received" while the pool may be zero. Remove it and the contributor leg becomes an open share of profit, divided by weights. That reads like a profit right, which is the dividend route this repo has already rejected for a fee. The investor leg breaks too: the split between contributors and lenders is computed from the remaining contributor ceilings, so with no ceiling there is no formula for that split. Any version of this idea must say what takes the ceiling's place.

**5. The ecological number must never be expressed in euros.** If damage is priced in euros, and those euros are converted into points and then into `p`, the rule prints a euro-per-`p` rate that is the same for everyone on a date. That is exactly the conversion rate every path in this repo refuses. Keep the measure physical, or an index. Do not publish the conversion.

**6. The mint curve makes the signal fade on its own.** The curve gives less weight per point as total points grow. The same damage, converted later, mints far fewer `p`, while the total stock keeps growing. The share burned each year would then shrink without anyone deciding that. If a proportional haircut is wanted, state the share directly instead of routing it through the curve.

**7. The cost lands on everybody, not on the cause.** A contributor who did nothing loses the same share as the project that caused the damage. If the aim is to change behaviour, the burn should follow the products and projects that caused it. That is the same move the scoped-royalty path makes for value.

**8. Who sets `k_eco`, and one conflict to record now.** A general assembly parameter fits the existing pattern, because the cap multiple and the opening factor are already policy parameters. But the people voting are the people whose weight is burned. A low `k_eco` mainly protects today's holders against tomorrow's contributors. Keep the existing rule that a parameter change works forward only, and keep the split between the two legs a formula that nobody votes on.

**9. Keep the regeneration mint proportional.** Proportional means a retired position stays at zero, because a share of nothing is nothing. A mint per head, or to everyone on the register, would bring back weight for work that was already paid for. That is the seniority hole from 2026-09-08.

**10. The independent institutions need naming before any specification.** Which body, which standard (life-cycle assessment, LCA), who pays for it, how often it runs, and what happens when two bodies produce different numbers. A number from outside that decides what people receive has to be fixed in the contract before the year starts, not chosen afterwards.

On the mission test, this is the strongest sketch in the folder so far. Its story is the mission itself, not a tax result and not private profit. That is worth keeping. It does not yet answer the tax question, and mission fit has never been a tax box.

## Decisions

None. The sketch stays **open**. It does not replace the live ceiling or the live burn. No ADR. No row on the path map and no folder yet, so this is a log entry only.

## Open Questions

- If documented effort goes, what bounds what a contributor may be paid, and what carries the arm's-length argument?
- Does the ecological factor belong on the yearly pool, where it changes euros, rather than on the weights, where it does not?
- Which unit is the destruction number in, and relative to what: revenue, one product, or a baseline year?
- One number for the whole company, or one per product and per project?
- Who are the independent institutions, which standard do they use, who pays, and how is a disagreement settled?
- How does the split between contributors and lenders work with no remaining contributor ceiling?
- Does a vote on `k_eco` stay a policy parameter, or does it become a vote on this year's pay?
- Does regeneration mint weight to all holders, or to the people who did the regenerative work?

## Next Steps

- Keep the sketch in the log. The live specification keeps its ceiling and its burn.
- If this is pursued, run the pair check against the investor bond, and add a row on the [path map](../../token-system-design/README.md) before any folder.
- Try `k_eco` on the yearly pool on paper first, before changing anything about the weights.
- Keep the ecological number out of euros, and out of any published document, until counsel has seen it.
