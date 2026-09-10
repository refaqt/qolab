# 2026-09-10 — Startup-style unpaid shares, revaluations, MoU, then a contributor class

**Role(s):** finance, business-dev

**Status:** Same rejection as the cheap-share dead-end **if** share *count* tracks contribution. The “one cash share per contributing member” sketch stays **open**. Design input for counsel, not a ruling.

**Prevention rules applied:** [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not put a euro spot price on certificates](../mistakes/2026-09-03_unit-price-on-growing-pool.md). Token-engineering: facts beat labels. Companions: [no investors / informal](2026-09-10_no-investors-euro-shares.md); [tokens not shares / revisor](2026-09-10_tokens-not-shares-avoid-revisor.md).

## What happened

Asked how to do **the same as in normal startups**: you do not buy yourself in; new shares are **given** and need not be 100% paid; there are **revaluations** of share prices. Sketch: start with an **MoU** that there will be shares **based on the contribution**; later issue a **new share class** and **give** each contributor that share.

That mixes three different startup objects with a labour quota the cheap-share route already rejected.

### 1. What startups actually do

They do **not** mint shares every week in proportion to hours. Typical Delaware / Belgian BV fundraising:

| Object | What happens | What it is not |
| --- | --- | --- |
| **Founder shares** | At incorporation the company is worth ~nothing. Founders **subscribe** at par / a tiny cash inbreng. They *do* buy in; the ticket is small because FMV is small. Reverse vesting: they already own; the company may buy unvested shares back if they leave. | Free paper. A running printer of shares for this week’s work. |
| **Employee / advisor grants** | Discrete board grants. Options / warrants at **then-FMV** strike (Belgium: Optiewet if it fits). RSUs / free shares are **taxed as income** at vesting / grant. | Continuous `N = f(hours)`. |
| **New round** | **New** shares issued at a **new** price a buyer pays. Old shares keep their historical issue price. Ownership **%** dilutes. The 10× is company value, not 10× of someone’s contribution. | Rewriting the paid-in amount of old shares. A GA “setting” a share price with no buyer. |

Belgian fundraising uses the same reverse-vesting idea (already owned; leaver buy-back), not a promise to issue later in proportion to a points ledger.

### 2. A CV cannot “give” shares

Art. **6:39 WVV**: a share may only be issued **in ruil voor een inbreng**. There is no gratuitous CV share. “Given” is either:

- a **cash** inbreng (they did buy in, even at €0.01), or
- **inbreng in nijverheid** / inbreng of a work receivable (art. **1:8**: a commitment to supply labour, which is inbreng in natura) → founder/board report + **bedrijfsrevisor** (arts. **6:8**, **6:110**), valuation, tax on FMV at grant, then 30% on later dividends.

Honest inbreng in nijverheid is often **worse** than a contingent fee ([cheap-share-route.md](../../token-system-design/cheap-share-route.md); [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md)). Extra company-law teeth: the subscriber **owes** what they promised (art. **1:9**), including a **non-compete** for the duration of a nijverheid inbreng; the shares **lapse** on death or lasting incapacity (art. **6:11**, unless statutes say otherwise).

Creating a **new class** does not skip 6:39. Class L still needs an inbreng. A class whose **number** of shares is `f(contribution)` is the labour quota ([2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md)).

### 3. Unpaid is a debt, not a gift

Partly paid shares exist (BV default: fully paid unless statutes / issuance terms say otherwise, art. **5:125**; NV has a statutory minimum paid-up). The holder remains **debtor** for the unpaid amount (art. **1:9**). Creditors or a curator can call it. Transfer of unpaid shares keeps the transferor on the hook for years (BV art. **5:66**).

Never calling the unpaid slice so the “price” is zero is a sham if the real deal was work-for-equity. Tax looks at FMV of the shares received minus a real obligation to pay. An obligation nobody intends to call is not a real obligation.

Unpaid **cash** inbreng is also not how you avoid the revisor if the economic contribution is labour.

### 4. Revaluations

A funding round does **not** revalue old shares on the cap table. It prints **new** shares at a new issue price because a **third party paid**. Book *herwaardering* of assets is accounting; it does not change who owns what.

A CV GA that “sets” a share price for uittreding / phantom / put is **not** a market ([tokens-not-shares](2026-09-10_tokens-not-shares-avoid-revisor.md) §5). NAV per labour-quota share is how class A drains the CV ([2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md)).

Without a buyer, there is nothing to revalue against. The startup 10× appears when **investors** (or a trade sale) pay a higher price for **new** paper, or when dividends follow a residual claim on a company that grew — not when the board restates €1 labour shares as €50.

### 5. MoU then “give each contributor that share”

An MoU that “there will be shares **based on the contribution**” is the [informal labour quota](2026-09-10_no-investors-euro-shares.md) with a letterhead. If it is non-binding, contributors have no share. If it is binding, it is a contractual claim for labour. Converting that claim into class L is inbreng of a *schuldvordering* / nijverheid → revisor + valuation of **past** work, and a benefit in kind of cheap paper.

Two readings of “each contributor is given that share”:

| Reading | Status |
| --- | --- |
| **N shares = f(how much they contributed)** | **Dead-end.** Same quota whether the ticket is €1, unpaid, or “given.” MoU + later class does not hide it. |
| **One share (or a fixed number) per person who contributed**, cash inbreng, count **not** `f(p)` | **Still open** as an option-1 membership sketch ([2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md); [tokens-not-shares](2026-09-10_tokens-not-shares-avoid-revisor.md) structure A). Contribution is an **eligibility** gate for membership, not a printer of extra paper. They still **subscribe** (small cash). Residual 10× is company value on that equal (or statutory-split) class. |

“Based on the contribution” in the MoU usually means the first reading. Write eligibility, not quantum, if the second is the intent.

### 6. What *does* look like a startup, in a CV

Keep **two instruments**. Do not mix them on one labour-minted class.

1. **Founder-like residual (option 1, capital).** A small set of people who should share company upside subscribe **cash** shares at t0 (or one cash share per later member). Negotiated **%**, reverse vesting / bad leaver in a members’ agreement — not hours × rate. New money, if any, buys a **different** class or the same class at a **new issue price** a buyer pays. Dividends: VenB first, 30% WHT, not deductible. No art. 49 on the dividend quantum if it holds as a return on shares.
2. **Ongoing work (option 2, fee).** `p` weights, contingent invoice, effort cap. Never convert `p` into shares. No revisor.

Warrants / Optiewet are a **BV/NV** path ([tokens-not-shares](2026-09-10_tokens-not-shares-avoid-revisor.md) §6). A **CV cannot** issue *inschrijvingsrechten* (art. **6:19**). Discrete FMV grants still do not scale as “one grant per contribution row.”

## Decisions

Proposed (not a new ADR): do not implement an MoU → unpaid / “given” contributor class whose number tracks work. That is still cheap-share. Unpaid and revaluation do not make it startup equity. Confirms [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md).

The open sketch remains: **equal** (or otherwise not-`f(p)`) cash membership shares beside option-2 credits.

## Open Questions

- Whether a statutory profit split between that membership class and an investor class is worth writing up — still open from [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md).
- Counsel: CV default on volstorting (parallel to BV art. 5:125); whether a “€0 called, €X unpaid” contributor class would be treated as nijverheid anyway.
- If a BV/NV vehicle is ever in scope for a real option pool, that is a different product (dilution, *voorkeurrecht*, Optiewet valuation), not QOLAB’s live spec.

## Next Steps

- Note this variant on [cheap-share-route.md](../../token-system-design/cheap-share-route.md).
- Start-off stays: equal cash membership + `p` weights + later invoices. An MoU, if any, should **not** promise shares in proportion to contribution.
- Counsel + accountant on the simpler option-2 spec, not on unpaid gifted class L.
