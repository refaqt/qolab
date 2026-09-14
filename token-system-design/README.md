# Token-system design — path map

QOLAB is a contribution-credit and governance system for work on Refaqt projects, in service of [Refaqt’s mission](../docs/mission.md) ([ADR 2026-09-14](../docs/decisions/2026-09-14_refaqt-mission-design-constraint.md)). This folder holds the working design. It is **design input for counsel and an accountant**, not a ruling and not a launched scheme.

Several distinct token systems have been sketched. This page says which one is live, which are open, which are parked, and which are dead. Each row has one entry document. Symbols: [glossary.md](glossary.md).

## Paths

| Path | Status | Mechanism in one line | Entry document |
| --- | --- | --- | --- |
| **Option 2 — contingent invoiced fee, `p` as weights** | **Live (next pass)** | Hours → `c` (weight scale) and `f` (invoice ceiling); `p = c0 · c^k` weights; yearly solvency-checked `P_t` split by `p`, clipped by the opened cap on documented effort; `p` amortizes by `alloc / rem`; nested mint budgets + project-as-contractor for sub-projects; effort target **~1×** | [paths/option-2-contingent-fee/](paths/option-2-contingent-fee/README.md) |
| **Scoped royalty / Cred-weighted euro-par Q** | **Viable; proposed base for the 10×** ([ADR 2026-09-14 two bases](../docs/decisions/2026-09-14_two-bases-10x-off-effort.md), Proposed) | Value-based split (Cred), royalty **scoped to the products that embody the contribution**; `1 Q = €1` coupon minted from that pool; invoice or self-bill; accepts tax at allocation | [paths/scoped-royalty-cred-q/](paths/scoped-royalty-cred-q/README.md) |
| **Cash-subscribed shares, count not `f(p)`** | **Open** (second instrument of structure A) | Equal share per contributing member, or a fixed statutory split against an investor class; real dividends; residual upside is company value; DVB **(q)** | [paths/cash-shares-residual/](paths/cash-shares-residual/README.md) |
| **Contract tokens** (phantom / revenue-share / warrants) | **Open, not pursued** | Contracts, not shares; still fees; arm’s length applies; warrants are a BV/NV path | [paths/contract-tokens/](paths/contract-tokens/README.md) |
| **Supplier-network access token** | **Open** | `p` receives a stream of an access token minted from OSS assets; the token gates supplier orders; no par | [paths/q-supplier-access/](paths/q-supplier-access/README.md) |
| **Vintage pools + time-opened lot cap** | **Parked (complexity)** | Analysis stands (no unit `v`, leftover to reserves, default-in, lots); packaging too heavy; if it returns, same burn per lot | [parked/vintage-pools.md](parked/vintage-pools.md) |
| **Cheap €1 shares** (+ five variants) | **Dead-end** | Share count = `f(p)` | [dead-ends/cheap-share-route.md](dead-ends/cheap-share-route.md) |
| **Bonding-curve shares with cheap grant value** | **Dead-end** | A steep curve mints almost everything at the origin | [dead-ends/README.md](dead-ends/README.md) |
| ***Inbreng in nijverheid* as later reward** | **Dead-end** | Needs a plan-ahead commitment and a revisor before issuance | [dead-ends/README.md](dead-ends/README.md) |
| **`S ← S − €` burn at euro par** | **Dead-end (sketch)** | 1 `S` = €1 | [dead-ends/README.md](dead-ends/README.md) |
| **`v = pool / N` unit price** | **Withdrawn** | Wait-and-run, idle pool, stacked VenB | [dead-ends/README.md](dead-ends/README.md) |

Cross-cutting: [analysis/belgian-tax-and-company-law.md](analysis/belgian-tax-and-company-law.md) (tax, VAT, company law, option 1 vs 2) and [analysis/dvb-questions.md](analysis/dvb-questions.md) (ruling catalog **(a)–(s)**). Spreadsheets for the 2026-09-03 and 2026-09-07 iterations: [spreadsheets/](spreadsheets/).

## Two bases, two tests (proposed)

The [2026-09-10 review](../docs/log/2026-09-10_arms-length-10x-and-repo-review.md) found that a multiple written as `k × hours × frozen band` hands the administration the comparable (hours × rate), so every euro above 1× must be defended as a risk premium on a wage-like benchmark. A royalty scoped to the products that use the contribution is compared against royalty rates instead, and a 10× lifetime return on the effort is then an ordinary outcome nobody computes. [ADR 2026-09-14 (Proposed)](../docs/decisions/2026-09-14_two-bases-10x-off-effort.md) therefore keeps option 2 at or near **1×** for time-based work and puts the 10×-shaped upside on the scoped-royalty path and/or on cash shares whose count is not `f(p)`. The gated option-2 10× stays documented as a fallback. Nothing is accepted until counsel and a DVB prefiling have looked at it.

## Binding constraints (all paths)

- [Refaqt’s mission](../docs/mission.md) is a design constraint: reject sketches whose only story is private profit extraction or a tax result.
- No **unit FX** on the mint: no `w = dc/dp` in euros, no `v = pool / N`, no 1 `p` = €1, no `S ← S − €`, no published `(k × E) / Δp` or `rem / p`. A ceiling is not consideration while `P_t` may be zero.
- No day-one lifetime multiple. Early-bird lives in the mint, not in waiting.
- Governance membership (small cash share) is **not** the reward. Share count never tracks contribution.
- Do not mix a dividend story and a fee on the same instrument. Pick the tax box first.
- Non-transferable, off-chain, no peer market. Employees stay on euro payroll.
- Do not publish 10×, `r`, a target ROI, or “beats ETFs” language anywhere.
- Cite **art. 53, 10° WIB 92** for the excess test and art. 49 for the conditions of deductibility ([mistake 2026-09-14](../docs/mistakes/2026-09-14_wrong-article-for-excess-test.md)).

## Adoption constraint

For a Belgian natural person, option 2 lands at roughly 63% combined levies; through a contributor BV at roughly 34% (VVPRbis 18%, or the liquidation reserve at ≈18% effective from 1 July 2026 where VVPRbis does not apply). The design therefore effectively requires every contributor to run a company. For a model whose premise is broad cooperative contribution, that is a product constraint, not a tax error. It is not solved by any path in this folder; the only sketch that would put a natural person near 34% without a BV is a dividend on labour-quota shares, which is a [dead-end](dead-ends/cheap-share-route.md). Numbers: [analysis §4](analysis/belgian-tax-and-company-law.md).

## Filing order

Take **(a)–(d)** to DVB prefiling as the box question. Expect the quantum (`k`) to come back as a condition (“provided the remuneration is at arm’s length”), not a confirmation; treat that as success. **(p)** is not the gate. Add **(r)** (exit / death) and **(s)** (scoped royalty) with the path that uses them. Full order: [dvb-questions.md § How to file](analysis/dvb-questions.md#how-to-file).

## Open questions (tracked where they belong)

| Question | Tracked in |
| --- | --- |
| Does the goal survive moving the 10× off the effort base onto a scoped royalty? | [ADR 2026-09-14 (Proposed)](../docs/decisions/2026-09-14_two-bases-10x-off-effort.md); [scoped-royalty path](paths/scoped-royalty-cred-q/README.md) |
| Can the ex-ante expected-value ≈ 1× argument be evidenced at launch, before any `P_t = 0` year? | [option-2 spec § Cap and opening](paths/option-2-contingent-fee/README.md); DVB **(p)** |
| Who bears an art. 53, 10° disallowance? | Pool absorbs — [annex-terms.md](paths/option-2-contingent-fee/annex-terms.md); [ADR 2026-09-14 defaults](../docs/decisions/2026-09-14_exit-death-and-disallowance-defaults.md) |
| Exit / death / succession of an unpaid opened cap | Continue as if present — [option-2 spec § Exit](paths/option-2-contingent-fee/README.md); DVB **(r)** |
| Art. 344 §1 exposure of the two-instrument split | DVB **(q)**; [cash-shares path](paths/cash-shares-residual/README.md) |
| Art. 6:1 WVV *coöperatief doel*; *werkende vennoot* strength; DVB appetite for confirming a quantum | [dvb-questions.md § Counsel items](analysis/dvb-questions.md#counsel-items-not-numbered-dvb-items) |
| Opening curve after month 12; oldest-lot-first vs junior/senior; sunset `T` | [option-2 spec § Open questions](paths/option-2-contingent-fee/README.md) |
| Which token letter for the access token vs the euro-par Q | [q-supplier-access](paths/q-supplier-access/README.md) |

Stack is not chosen. Default is an off-chain ledger, not a chain.
