# 2026-09-10 — €1 shares in proportion to contribution, no investors yet

**Role(s):** finance, business-dev

**Status:** Same rejection as the cheap-share dead-end. Not a new option. Design input for counsel, not a ruling.

**Prevention rules applied:** [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not put a euro spot price on certificates](../mistakes/2026-09-03_unit-price-on-growing-pool.md). Token-engineering: facts beat labels. Companion: [tokens not shares / revisor](2026-09-10_tokens-not-shares-avoid-revisor.md).

## What happened

Asked: if there are **no investors yet**, could contributors in the Refaqt CV just **buy €1 shares in proportion to how much they contributed**? And: what if that is **not put on paper yet**, just to start off?

That is the [cheap-share route](../../token-system-design/cheap-share-route.md) with two extra hopes: (1) no investor class, so a labour quota among ourselves is “just capital”; (2) staying informal so company-law and tax facts do not attach yet.

### 1. No investors does not save option 1

The cheap-share rejection was never “because B capital exists.” It was: **share *count* = `f(work)`**. Paying €1 is a ticket, not skin in the game ([ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md); [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md) at €0.10 vs €10).

Without investors, **all** residual profit is split by that labour quota. That is louder deferred pay, not a cleaner dividend. *Werkende vennoot* still wants real capital at risk in a joint enterprise, not a points printer on a €1 share. Allocation by contribution is the smoking gun that the cause is labour ([token-system.md](../../token-system-design/token-system.md) §3).

A CV share may only be issued **in ruil voor een inbreng** (art. 6:39 WVV). €1 cash is formally *inbreng in geld*. If how many shares you may buy is set by hours or `p`, the real contribution is work → *inbreng in nijverheid* (art. 1:8), which must be **valued** and typically needs a **bedrijfsrevisor**. That is the trigger the [tokens-not-shares](2026-09-10_tokens-not-shares-avoid-revisor.md) note was trying to avoid. Paying €1 does not turn labour into a cash contribution. Doing nijverheid honestly still cannot reward unplanned work later ([ADR 2026-09-10](../decisions/2026-09-10_inbreng-in-nijverheid-dead-end.md)).

**Later investors** do not freeze a fair start. Either they buy the same €1 class (they get the same dividend per share as people who already stacked a labour quota, or they buy a large cash stack and crowd labour), or you split classes and you are back at the 2026-09-08 €0.10 / €10 dead-end.

### 2. Not putting it on paper is worse, not a sandbox

Belgian shares in a CV exist when they are **issued**: statutes, register, paid-in cash (or valued inbreng). An informal “you will get N shares for this work” is **not** a share. It is a contractual claim for labour — option 2 / wage facts — without invoices.

It cannot be a **dividend**. Art. 18 WIB 92 needs a shareholder (or a profit right attached to membership) and a GA distribution after WVV tests. Splitting surplus with people who are not on the register is a fee, a hidden dividend, or both. Booking later as 30% WHT does not elect the box ([tokens-not-shares](2026-09-10_tokens-not-shares-avoid-revisor.md) §7).

**Papering later** is often the worst moment: converting the handshake into shares is inbreng of a *schuldvordering* / work-for-shares → revisor + valuation of past labour, and a benefit-in-kind of cheap paper for work already done. Unwritten promises can still bind (consensual contracts). They just lack corporate form, so departure, death, and new people have no register.

FPS look at facts, not at whether a notary has seen them. A ledger that already maps work → future share count is the quota.

Possible extra failure: informal cash to members with no invoice and no GA dividend can look like **art. 219** (*geheime commissielonen*) if the beneficiary is not identified correctly.

### 3. What *is* a start without investors or labour-quota paper

Keep **two instruments** ([tokens-not-shares](2026-09-10_tokens-not-shares-avoid-revisor.md) structure A; [ADR 2026-09-02](../decisions/2026-09-02_tax-aware-contribution-credits.md)):

| Start now | Do not start |
| --- | --- |
| Each contributing member buys the **same** small cash share (one €1 share, or a fixed number) for **governance**. *Inbreng in geld* → no inbreng-revisor. | Extra shares whose number tracks hours / points / `p`, on paper or in a side spreadsheet “until we incorporate it.” |
| Off-chain ledger of contribution **weights** (`p`). Contractually not parts/shares. No conversion into shares later. | Calling those weights “shares we have not issued yet.” |
| When there is cash: **invoice** as a contingent fee (option 2). | Informal profit splits “as if” we held proportional shares. |
| Residual profit, if any, by **shareholding that is not** `f(p)` (equal per member if everyone holds one share). Left open as an option-1 sketch on [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md). | Waiting to issue the labour quota once investors appear. |

The weights do not need to sit in the statutes to start. The membership share, if you issue one, should.

## Decisions

Proposed (not a new ADR): do not implement €1 labour-quota shares among contributors because there are no investors yet. Do not run that mapping off-register as a start. Confirms [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md). Next pass stays option 2 beside a small equal cash membership share.

## Open Questions

- Whether a statutory profit split on **equal** membership shares (not `f(p)`) is worth a separate option-1 sketch — still open from [2026-09-08](2026-09-08_option-1-tenth-vs-ten-euro-shares.md).
- Counsel: confirm that a side ledger of “future shares proportional to work” is already a quota / possible inbreng claim, even before issuance.

## Next Steps

- Keep the cheap-share route rejected; note this variant on [cheap-share-route.md](../../token-system-design/cheap-share-route.md).
- Start-off, if needed: equal cash membership + `p` weights + later invoices. Do not promise those weights will become extra shares.
- Counsel + accountant on the simpler option-2 spec, not on an informal labour-quota.
