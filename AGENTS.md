# Global Agent Rules

When entering a project, use progressive disclosure — do not bulk-load all docs.

## Default Read Policy

**Always read (if present):**

1. Project `AGENTS.md`
2. `<docs>/RULES.md` or `<docs>/rules.md` (`.agent/` or `.agents/` — use what exists)

**Read on demand:**

| Need | Read |
|------|------|
| Resume / compaction | `MEMORY.md` / `memory.md`, `CURRENT.md` / `current.md` |
| Regressions | `CURRENT` → `CHANGELOG` / `changelog.md` (newest entries only) |
| Deep implementation | `HANDOVER.md`, `DEEPDIVE.md`, `deepdive.md` |
| Deployment | `DEPLOYMENT.md`, `deployment.md` |
| Domain task | matching topic doc only |

Never require HANDOVER or full CHANGELOG for small tasks.

Project instructions override global instructions.

## Preferred Skills

When available, proactively load and use:

* project-agent-docs-manager

Use this skill whenever:

* A project contains AGENTS.md
* A project contains MEMORY.md
* A project contains HANDOVER.md
* A project contains CHANGELOG.md
* The user asks to initialize project documentation
* The user asks to continue previous work
* The user asks for project structure, documentation, deployment notes, handovers, changelogs, memory, or deep project context

## Development Rules

* Reuse existing routes, APIs, components, utilities, files, and patterns.
* Understand existing implementation before modifying it.
* Make the smallest safe change possible.
* Preserve existing behavior unless instructed otherwise.
* Do not assume architecture, deployment, or business logic.
* Do not invent facts, routes, commands, APIs, or deployment steps.
* Do not delete user work without permission.

## Documentation Rules

For meaningful changes:

* Update CHANGELOG.md.
* Update HANDOVER.md if work remains.
* Update MEMORY.md for durable context only.
* Update DEEPDIVE.md for important technical discoveries.

## Context Recovery

Do not rely on Git state for context recovery unless project docs say so or the user explicitly asks.

Prefer (on demand, not all at once):

1. Project `AGENTS.md` + rules doc
2. `CURRENT.md` / `current.md`
3. `MEMORY.md` / `memory.md`
4. `HANDOVER.md` / `handover.md`
5. `CHANGELOG.md` / `changelog.md` — newest entries only
6. `DEEPDIVE.md` / `deepdive.md`
7. Remaining `.agent/` or `.agents/` topic docs
8. Project files

## Responses

Always summarize:

* What changed
* Files modified
* Remaining work
* Risks or follow-ups
