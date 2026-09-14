# qolab

Token system for the governance and work on Refaqt projects.

## Setup

Clone with submodules, then from this repository root:

```bash
git clone --recurse-submodules https://github.com/refaqt/qolab.git
cd qolab
bash setup-tooling.sh
```

Humans on Windows may double-click `setup-tooling.bat` instead.

## Where to read next

- [AGENTS.md](AGENTS.md) — entry point for Cursor, Claude Code, and other agents
- [docs/onboarding.md](docs/onboarding.md) — how to set up and navigate this repository
- [docs/mission.md](docs/mission.md) — Refaqt mission (binding constraint on token and legal design)
- [docs/architecture.md](docs/architecture.md) — purpose and layout
- [token-system-design/README.md](token-system-design/README.md) — **path map**: every token system, its status, its entry document
- [token-system-design/paths/option-2-contingent-fee/](token-system-design/paths/option-2-contingent-fee/README.md) — the live spec (contingent invoiced fee, `p` as weights) and its [annex terms](token-system-design/paths/option-2-contingent-fee/annex-terms.md)
- [token-system-design/paths/scoped-royalty-cred-q/](token-system-design/paths/scoped-royalty-cred-q/README.md) — scoped royalty / Cred-weighted Q, proposed base for the large upside ([ADR 2026-09-14](docs/decisions/2026-09-14_two-bases-10x-off-effort.md), Proposed)
- [token-system-design/analysis/belgian-tax-and-company-law.md](token-system-design/analysis/belgian-tax-and-company-law.md) — Belgian tax/legal analysis
- [token-system-design/analysis/dvb-questions.md](token-system-design/analysis/dvb-questions.md) — questions **(a)–(s)** for the ruling commission
- [docs/log/2026-09-10_arms-length-10x-and-repo-review.md](docs/log/2026-09-10_arms-length-10x-and-repo-review.md) — review of the whole analysis; arm's length and the 10× cap
- [token-system-design/parked/vintage-pools.md](token-system-design/parked/vintage-pools.md) — vintage pools (parked: complexity)
- [token-system-design/dead-ends/](token-system-design/dead-ends/README.md) — every rejected sketch and the one fact that kills it
