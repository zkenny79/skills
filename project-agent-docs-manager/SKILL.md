---
name: project-agent-docs-manager
description: Initialize or slim agent project docs (AGENTS.md, .agent/.agents/). Use when setting up, auditing, or reducing tokens in agent documentation, memory, handover, or changelog files.
disable-model-invocation: true
---

# Project Agent Docs Manager

Agent continuity with **minimal default token cost**.

## Principle

Progressive disclosure: tiny entry docs first; depth on demand only.
Details: [reference.md](./reference.md) (file rules, templates, full workflows).

## Before Editing

1. Use existing `AGENTS.md`, `README.md`, `.agent/` or `.agents/` — no parallel doc trees.
2. Source of truth: project docs + chat + file scans (Git only if docs say so).

## Layout

| Location | Files |
|----------|-------|
| Root | `README.md`, `AGENTS.md` (<250 lines), optional tiny `CLAUDE.md` → AGENTS |
| `<docs>/` | `RULES`, `MEMORY`, `CURRENT`, `HANDOVER`, `CHANGELOG`, `DEPLOYMENT`; optional `CHANGELOG_ARCHIVE`, topic docs |

## Default Read Path (put in AGENTS.md)

**Always:** `AGENTS.md` + `<docs>/RULES.md`

**On demand:**

| Need | Read |
|------|------|
| Resume / compaction | `MEMORY`, `CURRENT` |
| Regressions | `CURRENT` → `CHANGELOG` |
| Deep implementation | `HANDOVER` |
| Deploy | `DEPLOYMENT` (+ target doc) |
| Domain task | matching topic doc only |

Never require `HANDOVER` or full `CHANGELOG` for small tasks.

## Workflows

**Audit:** `wc -l` on docs → shrink always-read files → move bulk out of `AGENTS.md` → archive old changelog → report before/after lines.

**Init:** Inspect project → compact root + docs set → merge existing docs → unknowns marked `Unknown`.

**Maintain:** Concise newest-first `CHANGELOG`; prune `CURRENT`; durable facts → `MEMORY` only.

## Safety

No deletes/overwrites without permission. No invented facts, paths, deploy details, or secrets.

## Response

Short: changes, files touched, whether default read path shrank, open unknowns.
