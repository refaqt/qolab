# Architecture

Refaqt’s mission is to make manufacturing use less resources and energy by making it more decentralized and local, more on-demand, and by democratizing access to manufacturing and manufacturing tools. Canonical text: [`mission.md`](mission.md). QOLAB is an instrument of that mission ([ADR 2026-09-14](decisions/2026-09-14_refaqt-mission-design-constraint.md)).

QOLAB is a **contribution-credit and governance system** for work on Refaqt projects. Several distinct token systems have been sketched; **no option is accepted yet.** The working design lives in [`token-system-design/`](../token-system-design/), organised by path. Start at the **path map**: [token-system-design/README.md](../token-system-design/README.md).

| Path | Status | Entry |
| --- | --- | --- |
| Option 2 — contingent invoiced fee, `p` as weights (effort target ~1×; lots; fractional `p` burn; nested mint budgets; project-as-contractor) | **Live (next pass)** | [paths/option-2-contingent-fee/](../token-system-design/paths/option-2-contingent-fee/README.md) |
| Scoped royalty / Cred-weighted euro-par Q | **Viable; proposed base for the large upside** ([ADR 2026-09-14](decisions/2026-09-14_two-bases-10x-off-effort.md), Proposed) | [paths/scoped-royalty-cred-q/](../token-system-design/paths/scoped-royalty-cred-q/README.md) |
| Cash-subscribed shares, count not `f(p)`; contract tokens; supplier-network access token | **Open** | [paths/](../token-system-design/README.md#paths) |
| Vintage pools + time-opened lot cap | **Parked (complexity)** | [parked/vintage-pools.md](../token-system-design/parked/vintage-pools.md) |
| Cheap shares (all variants), bonding-curve shares, *inbreng in nijverheid*, euro-par burns, `v = pool / N` | **Dead-end / withdrawn** | [dead-ends/](../token-system-design/dead-ends/README.md) |

Cross-cutting: [Belgian tax and company law](../token-system-design/analysis/belgian-tax-and-company-law.md); [DVB questions **(a)–(s)**](../token-system-design/analysis/dvb-questions.md); [glossary](../token-system-design/glossary.md). What a ruling can and cannot settle, and launching without one (consequences, cash reserve, look-back clocks): [2026-09-10 review](log/2026-09-10_arms-length-10x-and-repo-review.md), [2026-09-14 no-ruling log](log/2026-09-14_no-ruling-reserve-and-lookback.md).

**Accepted (design):** fractional burn of `p` against remaining opened cap ([ADR 2026-09-08](decisions/2026-09-08_p-burn-remaining-cap.md)); nested mint budgets ([ADR 2026-09-08](decisions/2026-09-08_nested-mint-budgets.md)); project-as-contractor cash path ([ADR 2026-09-09](decisions/2026-09-09_project-as-contractor.md)); the mission as a binding constraint ([ADR 2026-09-14](decisions/2026-09-14_refaqt-mission-design-constraint.md)). **Proposed:** two bases for the multiple ([ADR 2026-09-14](decisions/2026-09-14_two-bases-10x-off-effort.md)); exit / death / disallowance contract defaults ([ADR 2026-09-14](decisions/2026-09-14_exit-death-and-disallowance-defaults.md)).

**Adoption constraint.** For a natural person option 2 lands near 63% combined levies, through a BV near 34%; the design effectively requires every contributor to run a company. Product finding, not a tax error — [path map](../token-system-design/README.md#adoption-constraint).

Stack is not chosen yet. Default is an off-chain ledger.

## Repository layout

| Path | Role |
| --- | --- |
| `.agents/` | Shared agent rules and skills (`refaqt/refaqt-agents` submodule) |
| `doqs/` | Documentation tooling (`refaqt/doqs` submodule) |
| `.agents-local/` | Repo-specific agent rules and skills |
| `docs/` | Living documentation (this overview, mission, ADRs, log, mistakes) |
| `docs/mission.md` | Refaqt mission (binding constraint on token/legal design) |
| `token-system-design/README.md` | Path map: every token system, its status, its entry document |
| `token-system-design/analysis/` | Belgian tax / company-law analysis; DVB questions |
| `token-system-design/paths/<path>/` | One folder per token system (live, viable, open) |
| `token-system-design/parked/`, `dead-ends/`, `spreadsheets/` | Parked packaging; rejected sketches; calculation sheets |
| `AGENTS.md` | Agent entry point |
