# 2026-09-14 — Review follow-ups applied; design folder restructured by path

**Role(s):** finance, business-dev

**Prevention rules applied:** [no euro spot price on `p`](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [no day-one lifetime multiple](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [no labour-quota cheap shares](../mistakes/2026-09-04_cheap-share-euro-par.md); [no steep curve on a cheap grant](../mistakes/2026-09-07_steep-curve-low-grant.md); [retire paid-off `p`](../mistakes/2026-09-08_unburned-p-after-cap.md); [no *inbreng in nijverheid* for unplanned work](../mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md). No new text publishes 10×, `r`, or ROI language.

## What happened

Went through the [2026-09-10 repo review](2026-09-10_arms-length-10x-and-repo-review.md) item by item and applied everything that was still open (only the citation fixes in `dvb-questions.md` had been applied on 2026-09-10). Then restructured `token-system-design/` so that each distinct token system has one place and one status.

### Review items applied

| Review § | Done |
| --- | --- |
| 1.4 size vs shape | New §5 in the [Belgian analysis](../../token-system-design/analysis/belgian-tax-and-company-law.md) with the worked failure table and art. 206/3 §1; summarised in the option-2 spec §10 |
| 1.5–1.7 base of the 10× | [ADR 2026-09-14 two bases](../decisions/2026-09-14_two-bases-10x-off-effort.md) (**Proposed**): option 2 at or near 1×; the upside on a scoped royalty and/or cash shares; gated `k = 10` kept as fallback B with the §1.6 ex-ante argument and an evidence policy |
| 3.1 art. 49 vs 53, 10° | Fixed in place in the analysis note and the cheap-share note; dated citation note added to the four 2026-09-10 logs that used art. 49 / art. 26; [mistake 2026-09-14](../mistakes/2026-09-14_wrong-article-for-excess-test.md) |
| 3.3 ruling cannot settle `k` | Item 8 of the analysis note split: file for the box; (p) is not the gate |
| 3.5 VVPRbis eligibility, *auteursrechten* settled | Caveat under the option-1 vs option-2 table; one sentence on the upheld narrowing |
| 4.2 liquidation reserve | Extraction-route table in analysis §4 (VVPRbis 18% / liquidation reserve ≈18% / ordinary 30%) |
| 4.3 disallowance | **Pool absorbs** (Proposed) — [annex-terms.md](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md) §C, [ADR 2026-09-14 defaults](../decisions/2026-09-14_exit-death-and-disallowance-defaults.md) |
| 4.4 (i) leads with the ceiling | Mirrored in [p-burn-remaining-cap.md](../../token-system-design/paths/option-2-contingent-fee/p-burn-remaining-cap.md) |
| 4.5 exit / death | **Continue as if present** on death / successor; freeze on voluntary exit; lapse on exclusion — spec §8, annex §D, DVB **(r)**, same ADR |
| 4.6 natural person | “Adoption constraint” in the [path map](../../token-system-design/README.md) and `docs/architecture.md` |
| 4.7 not checked | “Counsel items” table at the end of [dvb-questions.md](../../token-system-design/analysis/dvb-questions.md) |
| Open questions | Tracked in the path map with a pointer each |
| New | DVB **(s)** scoped royalty; [mistake 2026-09-14 the multiple on the effort base](../mistakes/2026-09-14_10x-on-the-effort-base.md) |

### Restructure

`token-system-design/` now reads by path: [README.md](../../token-system-design/README.md) (path map with status per token system), [glossary.md](../../token-system-design/glossary.md), `analysis/` (Belgian tax and company law; DVB **(a)–(s)**), `paths/option-2-contingent-fee/` (live: consolidated spec, annex terms, `p` burn, nested mint budgets), `paths/scoped-royalty-cred-q/` (viable, proposed base for the upside), `paths/cash-shares-residual/` (open), `paths/contract-tokens/` (open, not pursued), `paths/q-supplier-access/` (open), `parked/vintage-pools.md`, `dead-ends/` (index of every rejected sketch; cheap-share note), `spreadsheets/`. The two near-duplicate `architecture.md` files are gone: `docs/architecture.md` is a short overview that points at the path map. Logs, ADRs and mistakes keep their flat date-named layout; their indexes gained a Path column. All relative links were rewritten and checked.

## Decisions

Two **Proposed** ADRs, both for counsel: [two bases](../decisions/2026-09-14_two-bases-10x-off-effort.md) and [exit / death / disallowance defaults](../decisions/2026-09-14_exit-death-and-disallowance-defaults.md). Nothing accepted as the live spec; nothing unparked or revived. Option 2 remains the next pass.

## Open Questions

- Does the goal survive moving the 10× off the effort base? (The Cred/Q path is now written as the answer; counsel decides.)
- Can the ex-ante expected-value ≈ 1× argument be evidenced before any `P_t = 0` year, if fallback B is used?
- Art. 344 §1 on any two-instrument structure (DVB **(q)**); scoping and rate cap of the royalty (DVB **(s)**).
- Counsel items listed in [dvb-questions.md](../../token-system-design/analysis/dvb-questions.md).
- Which name the supplier-network access token gets.

## Next Steps

- Counsel + accountant on both Proposed ADRs and on the annex terms; then DVB prefiling for **(a)–(d)** with **(r)**, and **(s)** / **(q)** with the base that is pursued.
- Draft the *dienstenovereenkomst* + QOLAB annex from `annex-terms.md`; a Cred annex if the scoped-royalty path is pursued.
- Keep every new note inside the path map; add a row to it before adding a sketch.
