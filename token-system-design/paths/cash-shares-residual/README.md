# Cash-subscribed shares, count not `f(p)` (open)

**Status: open.** The second instrument of **structure A**: labour is paid as an option-2 contingent fee; residual company upside sits on **real shares bought for cash**, whose number does **not** track hours, points, or `p`. Not accepted; no ADR of its own. Named as one of the two possible homes of the large upside in [ADR 2026-09-14 (two bases, Proposed)](../../../docs/decisions/2026-09-14_two-bases-10x-off-effort.md). Design input, not a ruling.

**What moved off this path on 2026-09-14.** A **capped** investor return now has its own path — the [capped participating bond](../capped-participating-bond/README.md) — because a per-investor cap cannot ride on a dividend: a dividend must be equal per share inside a *soort*, so capping one holder and not another is not writable without a class per vintage or a share that amortises to nothing (§ "What stays dead"). This path therefore keeps two jobs, both still open: **governance** (the equal active-member share), and the **uncapped** capital base if a real 10× for capital is ever wanted. That second job is now a live question, because the bond's uplift is deducted and so is rate-capped by art. 55 WIB 92 — the large multiple cannot live on the deductible instrument. See [capped-participating-bond §6](../capped-participating-bond/README.md).

Sources: [tokens not shares §7 structure A](../../../docs/log/2026-09-10_tokens-not-shares-avoid-revisor.md), [startup-equity MoU §6](../../../docs/log/2026-09-10_startup-equity-mou.md), [cheap-share A/B classes and sunset §8.2](../../../docs/log/2026-09-11_cheap-share-ab-classes-sunset.md), [no investors / equal membership share](../../../docs/log/2026-09-10_no-investors-euro-shares.md), [€0.10 vs €10 shares (statutory split idea)](../../../docs/log/2026-09-08_option-1-tenth-vs-ten-euro-shares.md).

**Prevention rules applied:** [no labour-quota cheap shares](../../../docs/mistakes/2026-09-04_cheap-share-euro-par.md) — this path exists **only** because the count is not `f(p)`; [no *inbreng in nijverheid*](../../../docs/mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md) — cash *inbreng* only; [no euro spot price](../../../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md).

---

## Mechanism

Two shapes, both with **cash** *inbreng in geld* (no inbreng-revisor) and a count that is independent of contribution:

| Shape | Count rule | Where the residual goes |
| --- | --- | --- |
| **Active-member equal share** | One share (or a fixed number) per contributing member. Membership is tied to a statutory *hoedanigheid* (“active contributor”); losing it triggers *uittreding van rechtswege* (arts. 6:121–6:122 WVV) and the share is destroyed at its *scheidingsaandeel* (paid-in value, the CV default) | Equally among active members; rotates with participation |
| **Fixed statutory split** | A contributor class and an investor class with a fixed profit split in the statutes (e.g. 50/50 of distributable profit); inside the contributor class, equal per member | By the statutory ratio, then equally |

Contribution is an **eligibility gate**, never a quantum. Dividends are genuine option-1 distributions: VenB first, GA decision after WVV net-asset and liquidity tests, 30% RV (18% VVPRbis where the shares qualify; the liquidation reserve gives a BV holder ≈18% otherwise), not deductible, no VAT. The 10× here is **10× of company value or paid-in capital**, like founder stock, never 10× of hours.

## Design rule against art. 344 §1

The whole political motive for the two-instrument split is that contributors who work more should also get more of the residual. The moment share allocation correlates with contribution — in the statutes, a members’ agreement, an MoU, or only in practice — the split into two legal boxes looks chosen for its tax result and the general anti-abuse rule can unwind it (DVB **(q)**). So:

- The count must be defensibly **not** `f(p)` for a reason that would hold if the tax outcome were reversed. That reason is [Refaqt’s mission](../../../docs/mission.md) written into the statutes as *doel* / *voorwerp* (art. 6:1 WVV *coöperatief doel*) plus the governance leg (a class ceiling on any financial class, the veto share, the asset lock — [governance-voting](../governance-voting/README.md)) and admission policy — not only governance convenience.
- No document ties share count to hours, points, `p`, or the contribution ledger. Credits never convert into shares.
- “More hours → more dividend” is **not** available on this instrument. That leg stays option 2.

## What stays dead

Every share whose number is `f(work)`: cheap €1 shares, €0.10 / €10 classes, a €1 / €100 pair with a linear quota, an informal or MoU ledger of future shares, unpaid or “given” shares, revaluations without a buyer, *inbreng in nijverheid* for unplanned work — [dead-ends](../../dead-ends/README.md). Warrants / *inschrijvingsrechten* are not a CV tool (art. 6:19) — [contract tokens](../contract-tokens/README.md).

## Open questions

- Whether this sketch is worth its own statute draft (open since 2026-09-08).
- Whether **two bases for capital** is pursued: a modest, deductible `k_I` on the [bond](../capped-participating-bond/README.md) beside genuinely uncapped equity here — the mirror of the two-bases answer already taken for labour.
- Counsel: art. 6:1 *coöperatief doel* of a CV whose main activity is rewarding contributor labour; whether *uittreding van rechtswege* on loss of the “active contributor” *hoedanigheid* is a clean mechanism and how the distribution tests apply to paying the *scheidingsaandeel*.
- Counsel: leonine-clause exposure (art. 4:2 WVV) of any class with a bounded profit right; VVPRbis *voorkeurrecht* test (art. 269 §2 WIB 92) between classes.
- Whether to seek NRC recognition or *erkend als sociale onderneming* — art. 8:5 WVV’s ~6% cap on patrimonial advantage fights a 10× residual ([mission.md](../../../docs/mission.md)).
- FSMA *informatienota* if an investor class is offered beyond members.
- DVB **(q)**: what correlation between contribution and share count is tolerated (eligibility gate vs quantum).
