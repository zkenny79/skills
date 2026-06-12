---
name: project-agent-docs-manager
description: Initialize, slim, or migrate agent project docs (AGENTS.md, .agent/). Use when setting up agent documentation, reducing doc token cost, or migrating legacy CHANGELOG/CURRENT/HANDOVER setups to the minimal model.
disable-model-invocation: true
---

# Project Agent Docs Manager

Agent continuity with **minimal token cost**. Git history is the record —
docs carry only what git cannot.

## Principle

Few files, all short, read on demand. Every doc line costs tokens on every
future read. Details: [reference.md](./reference.md).

## The File Set

| File | Purpose |
|------|---------|
| `AGENTS.md` (root) | Operating contract: read-on-demand table, git rules, project shape, non-negotiables, verify commands (~60 lines) |
| `CLAUDE.md` (root) | Thin import only: `@AGENTS.md` — never divergent content |
| `<docs>/RULES.md` | Short strict rulebook (workflow + hard rules + docs layout) |
| `<docs>/MEMORY.md` | Durable findings in short form: conventions, gotchas, env quirks |
| `<docs>/OVERVIEW.md` | The one deep reference: architecture, settings keys, API catalog, sharp edges |
| `<docs>/DEPLOYMENT*.md` | Optional, only if the project deploys: targets, exclusions, tag step |

`<docs>` = existing `.agent/` or `.agents/`; default `.agent/`. **No**
CHANGELOG, CURRENT, HANDOVER, DEEPDIVE, or topic docs.

## What Replaces The Deleted Files

- CHANGELOG → detailed commit messages (subject + why, one topic per commit)
- CURRENT → `git log --oneline -20` + MEMORY for anything durable
- HANDOVER → merged into OVERVIEW (deduplicated, stale facts fixed)
- Deploy history → annotated git tags `deploy/<target>-<yyyymmdd>`

## Workflows

**Migrate (legacy → minimal):** read legacy docs → merge unique valuable
content into OVERVIEW/MEMORY (fix stale facts while merging) → delete legacy
files via `git rm` (recoverable) → update all cross-references → add the
detailed-commit + deploy-tag rules to RULES → report line delta.

**Init:** inspect project → create AGENTS (+ CLAUDE import), RULES, MEMORY,
OVERVIEW; DEPLOYMENT only if deployment exists → unknowns marked `Unknown`.

**Audit:** `wc -l` on all docs → shrink AGENTS below ~80 lines → move depth to
OVERVIEW → cut anything git already answers → report before/after.

## Safety

Delete only what the user approved (git makes it recoverable — say so).
Merge before deleting; never lose unique facts. No invented facts, paths,
deploy details, or secrets in docs.

## Response

Short: files created/merged/deleted, line delta, what replaced what, open unknowns.
