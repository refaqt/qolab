# Onboarding

How to set up, run, and navigate this repository.

## Prerequisites

- Git (clone with `--recurse-submodules`)
- Bash (agents run `bash setup-tooling.sh` on any OS)
- Python 3 (DOQS validators and root-tool installer)

## Setup

1. Clone the repository (with submodules): `git clone --recurse-submodules https://github.com/refaqt/qolab.git`
2. Copy helpers from `doqs/templates/setup-tooling/` to the **repo root** if this is a new repo (never run them from the templates folder). Agents: `bash setup-tooling.sh`. Humans on Windows may double-click `setup-tooling.bat`.
3. This repository is a token/governance project, not a hardware machine. Do not scaffold `cad/`, `bom/`, `modules/`, or `okh.toml` unless that scope is explicitly requested.

## Where to read next

| Doc | Use |
| --- | --- |
| `docs/architecture.md` | Pointer to the working design |
| `token-system-design/` | Bonding-curve draft, spreadsheet, Belgian tax/legal analysis |
| `.agents-local/skills/patterns/SKILL.md` | Project-specific reusable patterns |
| `docs/decisions/` | Past technical decisions (ADRs) |
| `docs/mistakes/` | What went wrong and how to avoid it |
| `docs/log/` | Chronological activity log |
| `.agents/` | Shared agent rules and skills (refaqt-agents) |

## Cursor / Agent

Root `AGENTS.md` is the entry point. Shared rules/skills live in `.agents/`; Cursor adapters may live under `.cursor/rules/`. Prefer project guidance over duplicate User Rules in Settings.
