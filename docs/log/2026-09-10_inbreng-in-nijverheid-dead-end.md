# 2026-09-10 — Inbreng in nijverheid (dead-end)

**Role(s):** finance, business-dev

**Prevention rules applied:** [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not put a euro spot price on certificates](../mistakes/2026-09-03_unit-price-on-growing-pool.md). Token-engineering: labels do not take compensation outside VAT or income tax; facts beat labels.

## What happened

Asked whether shares for work could go through **inbreng in nijverheid** (art. 1:8 WVV) without a bedrijfsrevisor on every contribution: bless **hours × rate** once, then apply it whenever shares unlock; or send the revisor a list of work, hours, and shares issued. Wanted a light cadence (how many times a year, cost). Then asked whether the contributor must **promise** the work first and the revisor checks **afterwards**, or also **beforehand**. Then whether the cooperative must know **exactly** in advance how many contributors, which rates, and how many hours.

Working answers (design input for counsel, not a ruling):

- *Inbreng in nijverheid* **is** *inbreng in natura*. Each issuance needs a **board report** plus a **bedrijfsrevisor report** (CV: arts. 6:8 / 6:110; BV: 5:7 / 5:133). Missing reports → **null**. Shareholders cannot waive this. A standing method is not a licence. The six-month reuse exemption is for the **same already-valued assets**, not for a new batch of hours or a new person.
- Hours × a market band can be the board’s method. The revisor still examines **this round’s** people, hours, and share count **before** those shares exist. Sending a list is the **input** to the reports, not a substitute. Issue-then-email is the wrong order.
- True nijverheid is a **commitment to future work**, not a timesheet of hours already done. Sequence: **promise → revisor on the promise → shares → work** (delivery is *volstorting*; lapse / suspension if they cannot perform — art. 6:11 WVV for a CV). The revisor does not tick hours afterwards. Past hours unlocking shares is a different object (often a receivable) and still needs the revisor **before** issuance.
- You do **not** need a forever census of every future contributor. You **do** need, for each issuance, who is in that round, a **bounded** commitment per person, and a justified rate. An open “whoever logs hours, unlock shares” scheme cannot be valued. A yearly batch is still revisor-before-issuance for that batch. Typical report cost is on the order of **€1,500–€5,000** per round, plus filing / possible notary — not zero, and it repeats.
- Hours × rate also makes the share value **ascertainable at grant** (tax now, then 30% on later dividends if the dividend box holds). Often worse than a contingent fee. Share count = *f(hours)* remains a labour quota ([cheap-share euro par](../mistakes/2026-09-04_cheap-share-euro-par.md)).

QOLAB wants to **reward later**, after work exists, **without** people planning headcount, rates, and hours in advance. That is the opposite of the nijverheid sequence. Rejected: [ADR 2026-09-10](../decisions/2026-09-10_inbreng-in-nijverheid-dead-end.md). Logged in [docs/mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md](../mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md).

## Decisions

Rejected (dead-end): using *inbreng in nijverheid* (or a one-time method blessing, or a post-hoc hours list) to issue shares as the contribution reward. Still bound by the cheap-share rejection ([ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md)): labour-quota shares as the reward, and a grant-time valuation. Next pass stays option 2 with less machinery. Avoiding the inbreng-revisor remains: **do not issue (or convert into) shares for the work**; small cash membership share for voting ([tokens-not-shares log](2026-09-10_tokens-not-shares-avoid-revisor.md)).

## Next Steps

- Iterate option 2 with reduced complexity (not this path, not cheap extra shares, not bonding-curve shares).
- Counsel + accountant after that simpler spec exists. Do not promise anyone shares against a work commitment or a timesheet.
