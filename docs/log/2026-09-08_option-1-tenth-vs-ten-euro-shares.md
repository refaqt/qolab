# 2026-09-08 — Option-1 €0.10 vs €10 shares with a `p`-quota

**Role(s):** finance, business-dev

## What happened

Tried option 1 again so contribution and capital would share dividends more evenly, instead of capital taking surplus only because it paid more. Two CV share classes; dividend by **number of shares**, not by euros paid in. Class A at **€0.10**, members may **buy** according to `p`. Class B at **€10**, for investors. Shareholders are private persons, not employees. No retrieval cap and no burn yet. A 0.1 vs 1,000 split was considered first; switched to 0.1 vs 10.

Company law can write this (statutes, two soorten, profit per share). Option 1 still fails: share *count* = `f(p)` is the same labour quota as the €1 cheap-share dead-end. Paying €0.10 is a smaller ticket, not more skin in the game. The 100:1 issue-price gap is a chosen **FX** (conversion rate, as in foreign exchange) between labour and capital (one unit of `p` plus ten cents gets the same dividend as €10 of investor cash), not equality of two capital classes.

Dropping the old cap/burn makes the A share look more like a share (you keep it and keep getting dividends). It does not fix the quota. It also leaves no bound on what labour can take, and unbounded dilution of B whenever someone mints `p` and buys A shares. If voting is per share, A outvotes B as soon as enough cheap paper is issued. Exit (uittreding) per share of NAV lets A drain the CV; exit per euro of inbreng pays A holders their dimes back and leaves the dividend as the whole economic story.

Private persons and “no employees” help a little on RSZ employment only if there is no subordination. They do not turn a points-quota dividend into a capital return. Recharacterisation still stacks VenB at Refaqt (dividend not deductible) with professional tax on the natural person.

Same prevention rule: [cheap-share euro par](../mistakes/2026-09-04_cheap-share-euro-par.md). Not a new incident. Confirms [ADR 2026-09-04](../decisions/2026-09-04_cheap-share-route-dead-end.md). Note added on [cheap-share-route.md](../../token-system-design/cheap-share-route.md).

If labour and capital should both eat **without** a points printer: a statutory split (for example 50/50 of distributable profit; inside A, one share per contributing member). If `p` must scale what someone takes, that leg is option 2 and B shares stay ordinary capital.

## Decisions

Proposed (not accepted): do not implement €0.10 vs €10 labour-quota shares as option 1. Changing the ticket price and dropping the burn does not win 30% dividend treatment. Next pass stays option 2 with less machinery.

## Open Questions

- Whether a statutory profit split between a **membership** class (not `f(p)`) and an investor class is worth a separate option-1 sketch.
- Retrieval cap for the option-2 pass still open (documented effort vs hours × one reference €/h vs time-fade of weights).

## Next Steps

- Iterate option 2 with reduced complexity (not this two-class quota, not cheap extra shares, not an `S − €` burn).
- Counsel + accountant after that simpler spec exists.
