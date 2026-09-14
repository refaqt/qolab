# qolab repository profile

QOLAB is a **token system** for the governance and work on Refaqt projects. It is not a hardware machine repository.

## Mission

Refaqt’s mission is to make manufacturing use less resources and energy by making it more decentralized and local, more on-demand, and by democratizing access to manufacturing and manufacturing tools.

Canonical text and how to apply it: [`docs/mission.md`](../../docs/mission.md). **Before** token-system, statute, DVB, or legal drafting, read that file and reject sketches whose only story is private profit extraction or a tax result.

## Conventions

- Shared agent rules and skills: `.agents/` (`refaqt/refaqt-agents`).
- Documentation tooling: `doqs/` (`refaqt/doqs`).
- Repo-specific guidance: this file and `.agents-local/skills/`.
- Living docs: `docs/mission.md`, `docs/architecture.md`, `docs/decisions/`, `docs/log/`, `docs/mistakes/`.
- Token-system design lives in `token-system-design/`, one folder per path; the path map `token-system-design/README.md` lists every token system with its status. New sketches get a row there and a path note (or a dead-ends row), never a loose file at the folder root.
- Cite art. 53, 10° WIB 92 for the excess test and art. 49 for the conditions of deductibility (`docs/mistakes/2026-09-14_wrong-article-for-excess-test.md`). Never publish 10×, `r`, or ROI language. **Two carve-outs only:** a contracted contributor's statement of their own ceiling (`token-system-design/paths/option-2-contingent-fee/annex-terms.md` clauses 24–27), and an investor offering document stating `r_I`, `k_I` and the cap and nothing about the contributor leg (`docs/decisions/2026-09-14_investor-leg-capped-participating-bond.md`). The two instruments never appear in one document.
- Before adding a **second instrument**, check it against the first as a pair: list the facts the first instrument's defence relies on being *absent* and confirm the second does not supply one, including in documents the company is compelled to publish (`docs/mistakes/2026-09-14_second-instrument-publishes-the-comparable.md`).
- Do not create DOQS machine folders (`cad/`, `bom/`, `modules/`, `firmware/`, `okh.toml`) unless that scope is explicitly requested.

## Stack

Not yet chosen. Record stack decisions as ADRs under `docs/decisions/`.
