# Global Agent Rules

When entering a project, read in this order if present:

AGENTS.md → RULES.md → MEMORY.md → HANDOVER.md → CHANGELOG.md → DEEPDIVE.md → .agents/

Project instructions override global instructions.

## Preferred Skills

When available, proactively load and use:

* project-operating-system

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

Do not rely on Git state for context recovery unless explicitly requested.

Prefer:

1. HANDOVER.md
2. CHANGELOG.md
3. MEMORY.md
4. DEEPDIVE.md
5. .agents/
6. Project files

## Responses

Always summarize:

* What changed
* Files modified
* Remaining work
* Risks or follow-ups
