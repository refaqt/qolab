# Architecture

System overview and component map for this repository. Update when layout, entry points, or major modules change.

## Purpose

Token system for the governance and work on Refaqt projects.

## Repository layout

| Path | Role |
| ---- | ---- |
| `.agents/` | Shared agent rules and skills (`refaqt/refaqt-agents` submodule) |
| `doqs/` | Documentation tooling (`refaqt/doqs` submodule) |
| `.agents-local/` | Repo-specific agent rules and skills |
| `docs/` | Living documentation (architecture, ADRs, log, mistakes) |
| `AGENTS.md` | Agent entry point |
