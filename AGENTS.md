# Agent guide

Entry point for Cursor, Claude Code, and other agents working in this repository.

## First step (required)

Before reading `.agents/` rules or skills, update tooling submodules to latest `main`:

- **All agents, any OS:** `bash setup-tooling.sh`
- **Humans on Windows** may double-click `setup-tooling.bat` (`pause` is OK there only). Agents must not run the `.bat`.

## Shared kit

This repo mounts [refaqt/refaqt-agents](https://github.com/refaqt/refaqt-agents) at [`.agents/`](.agents/).

1. Read [`.agents/rules/core.md`](.agents/rules/core.md) and [`.agents/rules/living-docs.md`](.agents/rules/living-docs.md).
2. Read [`docs/mistakes/`](docs/mistakes/) and state which prevention rules apply.
3. Read [`docs/architecture.md`](docs/architecture.md) before non-trivial work.
4. Before new coding solutions, check [`.agents-local/skills/patterns/SKILL.md`](.agents-local/skills/patterns/SKILL.md) if present.

## This repository

QOLAB — token system for the governance and work on Refaqt projects. Repo profile, folder map, and conventions: [`.agents-local/rules/repo.md`](.agents-local/rules/repo.md).

| You are adding | It goes in |
| --- | --- |
| A day's work write-up | `docs/log/YYYY-MM-DD_topic.md` |
| Why a choice was made | `docs/decisions/YYYY-MM-DD_topic.md` |
| Something that went wrong | `docs/mistakes/YYYY-MM-DD_topic.md` |

Repo-specific skills: [`.agents-local/skills/`](.agents-local/skills/).

## Skills

| Skill | Path |
| --- | --- |
| Activity log | [`.agents/skills/log/SKILL.md`](.agents/skills/log/SKILL.md) |
| Mistake log | [`.agents/skills/mistake-log/SKILL.md`](.agents/skills/mistake-log/SKILL.md) |
| Maintain patterns | [`.agents/skills/maintain-patterns/SKILL.md`](.agents/skills/maintain-patterns/SKILL.md) |
| Coding patterns | [`.agents-local/skills/patterns/SKILL.md`](.agents-local/skills/patterns/SKILL.md) |

## DOQS machine repos (when `doqs/` submodule is present)

1. Read `doqs/docs/architecture.md` for module layout, OKH, builds, simulation.
2. After structural changes: `python doqs/scripts/validate_all.py` from repo root.
3. Additional skills from this kit:

| Skill | Path |
| --- | --- |
| DOQS naming | [`.agents/skills/doqs-naming/SKILL.md`](.agents/skills/doqs-naming/SKILL.md) |
| FreeCAD debugging | [`.agents/skills/freecad/SKILL.md`](.agents/skills/freecad/SKILL.md) |

4. Repo-specific workflow rules → `.agents-local/rules/` (e.g. `doqs-workflow.md`).
5. Copy [`.agents/templates/cursor-rule-doqs-naming.mdc`](.agents/templates/cursor-rule-doqs-naming.mdc) and [`.agents/templates/cursor-rule-freecad.mdc`](.agents/templates/cursor-rule-freecad.mdc) to `.cursor/rules/` when using Cursor.
