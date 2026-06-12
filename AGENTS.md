# Global Agent Rules

When entering a project, use progressive disclosure — do not bulk-load docs.
Default workflow: search the relevant source files directly and make the
smallest safe change using existing patterns.

## Default Read Policy

**Always read (if present):** project `AGENTS.md` only.
`CLAUDE.md` should be a thin import of `AGENTS.md` (`@AGENTS.md`) so both stay
identical — one source of truth for every agent. If a project still has a
divergent CLAUDE.md, treat AGENTS.md as authoritative and suggest unifying.

**Read on demand:**

| Need | Read |
|------|------|
| Changing docs/rules/deploy behavior | `<docs>/RULES.md` |
| Resume / compaction | `<docs>/MEMORY.md` |
| Deep project context (architecture, settings, API catalog) | `<docs>/OVERVIEW.md` |
| Deployment | `<docs>/DEPLOYMENT.md` (+ target docs) |

`<docs>` is `.agent/` or `.agents/` — use what exists. Legacy files
(`CURRENT`, `HANDOVER`, `CHANGELOG`, `DEEPDIVE`, topic docs) may still exist in
older projects; do not maintain them — propose migrating via
project-agent-docs-manager.

Project instructions override global instructions.

## Git Is The Record

- Commit + push after meaningful changes. **Detailed commit messages replace
  changelogs**: precise subject + body with what changed and why; one topic per
  commit so `git log --oneline` reads as the feature history.
- Recover history via `git log --oneline`, `git log --grep`, `git log -S` —
  not via handwritten change docs.
- After every deploy, create an annotated tag `deploy/<target>-<yyyymmdd>`
  describing what was uploaded. `git log deploy/<tag>..HEAD` shows what a
  server is missing.

## Preferred Skills

When available, proactively load and use **project-agent-docs-manager** when:

* A project's agent docs need initializing, auditing, or slimming
* A project still carries legacy CHANGELOG/CURRENT/HANDOVER files
* The user asks for project structure, documentation, memory, or deep context

## Development Rules

* Reuse existing routes, APIs, components, utilities, files, and patterns.
* Understand existing implementation before modifying it.
* Make the smallest safe change possible; preserve behavior unless instructed.
* Do not assume architecture, deployment, or business logic.
* Do not invent facts, routes, commands, APIs, or deployment steps.
* Do not delete user work without permission.
* Verify beyond compile checks: syntax checkers miss runtime errors — smoke-test
  new module-level code with a real import/call.

## Documentation Rules

* No changelog, status, or handover maintenance — git history covers it.
* Update `MEMORY.md` only for durable facts that must survive compaction
  (conventions, gotchas, environment quirks) — never recent-change noise.
* Update `OVERVIEW.md` only when project fundamentals change.
* Keep every doc short; every line costs tokens on every future read.

## Context Recovery

In order, on demand — not all at once:

1. Project `AGENTS.md`
2. `<docs>/MEMORY.md`
3. `git log --oneline -20` (recent work)
4. `<docs>/OVERVIEW.md` (only if fundamentals are needed)
5. Project files

## Responses

Always summarize: what changed, files modified, remaining work, risks/follow-ups.
