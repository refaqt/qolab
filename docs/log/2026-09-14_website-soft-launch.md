# 2026-09-14 — Soft-launch: what the website may say before the legal drafting exists

**Role(s):** business-dev, finance, marketing

**Status:** Publication rule for a contributor-only trust test. No ADR. Does not accept, unpark, or revive anything. Does not open the investor leg. Design input for counsel, not a ruling and not an offer.

**Prevention rules applied:** [no euro spot price on `p`](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [no day-one lifetime multiple](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [no labour-quota cheap shares](../mistakes/2026-09-04_cheap-share-euro-par.md); [a second instrument must not publish the comparable](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md). Informal “shares later” is worse, not a sandbox — [2026-09-10](2026-09-10_no-investors-euro-shares.md). The website is public material: the contributor-statement and offering-document carve-outs do not apply.

## What happened

Asked how to put the contribution and investment framework on the website before counsel writes the Dutch contracts, so that:

- people can see how contribution and, later, capital are meant to work;
- the same text can be used when talking to contributors before they join;
- a small group can start on trust: log every accepted contribution, keep a first database.

Not asked: build the website, or take investment cash. The test is **contributors only**.

The live start-off was already the answer. Hours → weights `p` and documented effort `f`. Cash only later, as a contingent invoice if a pool exists. Skipping a DVB ruling is a [normal Belgian choice](2026-09-14_no-ruling-reserve-and-lookback.md). Skipping paper that matches the facts is not. An MoU that “there will be shares based on the contribution” is the [rejected labour quota](2026-09-10_startup-equity-mou.md).

The publication risk is the same pair already on the record:

1. A public page that states a return, a multiple, or euros per weight hands the administration a comparable and books a claim.
2. One page that explains **both** legs publishes the capital rate next to the labour ceiling — [2026-09-14 mistake](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md).

So the soft-launch is three layers, written as [publication-surfaces.md](../../token-system-design/paths/option-2-contingent-fee/publication-surfaces.md): a contributor page anyone can read; a talk-track with no numbers; a fact ledger plus a short contractor note for the named group. Capital, if mentioned at all, is a **second page that is not an offer**. Investor cash stays closed.

## Decisions

None as an ADR. Working rules for the website and the trust group (still for counsel):

- **Contributor page only** for the framework people join on. Terms are not final. Logged work is a record, not a claim.
- **No numbers** on public or promotional material: no `r`, `k`, 10×, ROI, remaining euros, or “you earn more if you wait.”
- **Two pages if capital is named at all.** Never one document. Do not take investment cash. Do not state `r_I` or `k_I` on the site.
- **Trust group = fact ledger + short contractor note**, not informal profit shares. Spreadsheet columns: person, project, description, hours, accept date, who accepted, band or `f`, `c = hours × 100`. Do not store remaining euros or a personal cap. Nobody invoices until a real pool exists.
- **Accountant instruction from day one:** do not book a ceiling ([annex clause 27](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md)).

## Open Questions

- Counsel: is a one-page contractor note enough before the full Dutch annex, for a named group that logs work and invoices nothing yet?
- Whether to publish the capital page at all before the bond is open. If in doubt, omit it.
- Values of `r` and `k`, the mint curve, and pool policy — unchanged; do not freeze them on the site.

## Next Steps

- Paste the draft contributor copy from [publication-surfaces.md](../../token-system-design/paths/option-2-contingent-fee/publication-surfaces.md) onto the public site. Keep the capital page off, or paste the “not an offer” draft on a **separate** URL.
- Open the spreadsheet with the columns in that note. Sign the short contractor note with the named group. Instruct the accountant not to book a ceiling.
- Counsel still drafts the Dutch *dienstenovereenkomst* and QOLAB annex. The website must not pretend that step is done.
