---
name: project-agent-docs-manager
description: Maintain a cross-platform project documentation system for AI agents using README, AGENTS, MEMORY, RULES, HANDOVER, CHANGELOG, DEPLOYMENT, DEEPDIVE, and .agents context files.
disable-model-invocation: false
---

# Project Agent Docs Manager

Use this skill whenever working on a project that should stay easy to continue across multiple AI agents, devices, editors, platforms, and context compaction.

This skill manages a project documentation system built around these root files:

```text
README.md
AGENTS.md
MEMORY.md
RULES.md
HANDOVER.md
CHANGELOG.md
DEPLOYMENT.md
DEEPDIVE.md
.agents/
```

The purpose is to make every project self-explaining, even when there is no Git repository, when chat context gets compacted, or when work moves between tools like Zed, Cursor, Codex, Claude Code, OpenCode, Devin, VS Code, or another AI agent platform.

## When to use this skill

Use this skill when the user asks to initialize, maintain, repair, audit, continue, or improve project documentation.

Also use it when the project already contains any of these files:

```text
AGENTS.md
MEMORY.md
RULES.md
HANDOVER.md
CHANGELOG.md
DEPLOYMENT.md
DEEPDIVE.md
.agents/
```

Use it before making project changes if the user clearly wants persistent project context, multi-agent workflows, context compaction safety, or no-Git local project continuity.

## Main rule

Before changing code or project files, read the project documentation first.

Default reading order:

```text
README.md
AGENTS.md
RULES.md
MEMORY.md
HANDOVER.md
CHANGELOG.md
DEEPDIVE.md
.agents/README.md
.agents/deepdive.md
.agents/references/
.agents/knowledgebase/
knowledgebase/
```

If some files do not exist, create them when initializing the docs system.

Never assume Git exists. Never rely on `git status` for context compaction unless the user explicitly asks for Git usage. Prefer `CHANGELOG.md`, `HANDOVER.md`, chat history, `.agents/`, and project files.

## Required documentation structure

At the project root, maintain:

```text
README.md
AGENTS.md
MEMORY.md
RULES.md
HANDOVER.md
CHANGELOG.md
DEPLOYMENT.md
DEEPDIVE.md
```

Inside `.agents/`, maintain:

```text
.agents/
├── README.md
├── deepdive.md
├── references/
├── handovers/
├── plans/
├── audits/
└── knowledgebase/
```

## File purposes

`README.md` is the general product-style readme, like a GitHub project page. It explains what the project is, what it does, features, setup, usage, folder structure, current status, and where deeper docs are located.

`AGENTS.md` is the main instruction file for AI agents. It explains the documentation system, the required reading order, the `.agents/` folder, project rules, and how future agents should continue work.

`MEMORY.md` stores durable context for context compaction. Include things like “no Git repository”, preferred workflows, useful commands, important project facts, known limitations, knowledgebase summaries, and long-term conventions. Do not dump every small change here.

`RULES.md` is the strict rulebook. It must include: always use existing routes and conventions, always update `CHANGELOG.md`, never rely on Git status for compaction unless explicitly asked, always check `CHANGELOG.md`, `HANDOVER.md`, chat history, and `.agents/`, do not invent deployment steps, do not overwrite user work without permission.

`HANDOVER.md` stores current in-progress state. It should say what is being worked on, what is unfinished, what needs fixing later, files touched, risks, and next steps. If nothing is unfinished, clearly say that.

`CHANGELOG.md` records every meaningful change. Every change must get a timestamped entry with summary, files changed, reason, and follow-up.

`DEPLOYMENT.md` documents deployment only when known. Include servers, domains, ports, service names, paths, restart commands, Cloudflare tunnels, Docker, systemd, VPS, Raspberry Pi, environment files, rollback, and troubleshooting. Do not guess.

`DEEPDIVE.md` contains deep project knowledge: architecture, routes, functions, APIs, data flow, workarounds, fragile areas, known issues, and important implementation details.

`.agents/README.md` explains the `.agents/` folder and how agents should use it.

`.agents/deepdive.md` stores detailed agent-specific notes, platform quirks, investigations, refactoring notes, and deeper observations that should not clutter the root docs.

`.agents/references/` stores long references, copied docs, API notes, product rules, or external context.

`.agents/handovers/` stores dated handover snapshots.

`.agents/plans/` stores plans before major or risky changes.

`.agents/audits/` stores audits, review notes, risk reports, and cleanup findings.

`.agents/knowledgebase/` stores local knowledgebase notes. Summarize durable facts from it in `MEMORY.md`.

## Workflow before project changes

1. Read the root docs.
2. Read `.agents/README.md` and `.agents/deepdive.md` if they exist.
3. Check `.agents/references/`, `.agents/knowledgebase/`, or `knowledgebase/` if relevant.
4. Identify existing routes, files, functions, styles, APIs, components, and conventions.
5. Make the smallest safe change.
6. Update `CHANGELOG.md`.
7. Update `HANDOVER.md` if anything is unfinished or important for the next agent.
8. Update `MEMORY.md` only if durable long-term context changed.
9. Update `DEEPDIVE.md` only if architecture, routes, functions, workarounds, or deep project knowledge changed.
10. Final response should summarize what changed and which docs were updated.

## Initialization workflow

When initializing this documentation system in a project:

1. Inspect the current project structure.
2. Do not assume Git exists.
3. Create missing root docs.
4. Create `.agents/` structure.
5. Preserve and merge existing documentation instead of overwriting it.
6. Add clear placeholders where project details are unknown.
7. Add the first `CHANGELOG.md` entry.
8. Add a real `HANDOVER.md` status.
9. Tell the user exactly what was created and what still needs filling in.

## Required contents for new files

When creating `AGENTS.md`, include this core instruction:

```markdown
# AGENTS.md

Before making changes, agents must read:

1. README.md
2. AGENTS.md
3. RULES.md
4. MEMORY.md
5. HANDOVER.md
6. CHANGELOG.md
7. DEEPDIVE.md
8. .agents/README.md
9. .agents/deepdive.md

Rules:
- Prefer existing routes, files, functions, APIs, components, styles, and conventions.
- Do not assume this project uses Git.
- Do not use Git status as the default context source.
- Always update CHANGELOG.md after meaningful changes.
- Update HANDOVER.md when work is incomplete or current status changes.
- Update MEMORY.md only for durable long-term context.
- Update DEEPDIVE.md when deep technical knowledge changes.
```

When creating `RULES.md`, include:

```markdown
# RULES.md

- Always use existing routes, files, functions, APIs, components, styles, and conventions where possible.
- Always document every meaningful change in CHANGELOG.md with a timestamp.
- Keep changelog entries clear and easy to understand.
- For context compaction, never rely on Git repository status unless explicitly asked.
- For context compaction, always check CHANGELOG.md, HANDOVER.md, chat history, and .agents/.
- Do not invent routes, endpoints, commands, configs, deployment paths, or server details.
- Do not delete or overwrite user work without permission.
- Before major rewrites, document the plan in .agents/plans/.
- After incomplete work, update HANDOVER.md.
```

When creating `MEMORY.md`, include:

```markdown
# MEMORY.md

This file stores durable project context for future agents and context compaction.

## Durable facts

- Git repository: Unknown. Do not assume Git exists.
- Context source priority: CHANGELOG.md, HANDOVER.md, chat history, .agents/, then project files.
- Preferred approach: use existing project routes, files, functions, styles, and conventions before creating new ones.

## Knowledge base context

If a knowledgebase folder exists, summarize its important contents here.

## Useful techniques

- Before changing code, inspect existing patterns.
- Before deployment changes, check DEPLOYMENT.md.
- For unfinished work, update HANDOVER.md.
- For every meaningful change, update CHANGELOG.md.
```

When creating `HANDOVER.md`, use:

```markdown
# HANDOVER.md

Last updated: YYYY-MM-DD HH:mm TZ

## Current status

No active unfinished work documented yet.

## In progress

- None.

## Recently changed

- Documentation system scaffold created.

## Needs attention later

- Fill project-specific details.

## Useful next steps

- Inspect project files and replace placeholders with real project information.
```

When creating `CHANGELOG.md`, use newest entries first and this entry format:

```markdown
# CHANGELOG.md

Newest entries first.

## YYYY-MM-DD HH:mm TZ — Change title

Agent/platform: Unknown
Status: Completed / Partial / Planned

Summary:
- Explain what changed.

Files changed:
- path/to/file

Reason:
- Explain why the change was made.

Follow-up:
- None, or list next steps.
```

When creating `DEPLOYMENT.md`, include:

```markdown
# DEPLOYMENT.md

This file documents confirmed deployment information only.

Do not guess deployment information.

## Current deployment status

Unknown.

## Servers and environments

| Name | Role | Host/IP | Path | Notes |
|---|---|---|---|---|

## Domains

| Domain | Purpose | Target |
|---|---|---|

## Services

| Service | Purpose | Restart command | Notes |
|---|---|---|---|

## Ports

| Port | Service | Public? | Notes |
|---|---|---|---|

## Environment files

| File | Purpose | Notes |
|---|---|---|

## Deployment steps

Add confirmed deployment steps here.

## Rollback

Add rollback steps here once known.

## Troubleshooting

Add known deployment issues and fixes here.
```

When creating `DEEPDIVE.md`, include:

```markdown
# DEEPDIVE.md

This file contains deep project knowledge.

## Architecture

Unknown.

## Important routes

No routes documented yet.

## Important functions and modules

No functions documented yet.

## Data flow

Unknown.

## Existing workarounds

No workarounds documented yet.

## Fragile areas

No fragile areas documented yet.

## Known issues

No known issues documented yet.

## Useful implementation notes

Add useful project-specific notes here.
```

When creating `.agents/README.md`, include:

```markdown
# .agents

This folder stores agent-specific working context.

Root docs should stay readable and stable. Detailed plans, audits, investigation notes, references, knowledgebase notes, and temporary handovers can live here.

## Structure

.agents/
├── README.md
├── deepdive.md
├── references/
├── handovers/
├── plans/
├── audits/
└── knowledgebase/

## Agent workflow

1. Read root docs.
2. Read this file.
3. Read .agents/deepdive.md.
4. Check relevant subfolders.
5. Make changes.
6. Update CHANGELOG.md.
7. Update HANDOVER.md if needed.
```

When creating `.agents/deepdive.md`, include:

```markdown
# .agents/deepdive.md

This file contains detailed agent-facing project knowledge.

Use it for:
- Investigation notes.
- Platform-specific behavior.
- Local environment quirks.
- Prompting notes.
- Refactoring notes.
- Deep implementation observations.

## Current notes

No agent-specific deep notes yet.
```

## Changelog rules

Every meaningful project change must update `CHANGELOG.md`.

A meaningful change includes:

* Code edits.
* Config edits.
* Route changes.
* Deployment changes.
* Documentation changes.
* File moves.
* Bug fixes.
* Refactors.
* New features.
* Removed features.
* Changed behavior.

Use this format:

```markdown
## YYYY-MM-DD HH:mm TZ — Short title

Agent/platform: Zed / Cursor / Codex / Claude / Unknown
Status: Completed / Partial / Planned

Summary:
- Clear explanation of what changed.

Files changed:
- `file/path.ext`

Reason:
- Why this was done.

Follow-up:
- None, or list what remains.
```

## Handover rules

Update `HANDOVER.md` when:

* Work is incomplete.
* There are unresolved bugs.
* There are files that need review later.
* A deployment still needs testing.
* The next agent needs to know what happened.
* The current project state changed significantly.

If everything is complete, say:

```markdown
No active unfinished work.
```

## Context compaction rules

For context compaction, do not check Git repository status by default.

Instead, use:

1. `CHANGELOG.md`
2. `HANDOVER.md`
3. Chat history if available
4. `.agents/`
5. `MEMORY.md`
6. `DEEPDIVE.md`
7. Relevant project files

Summarize only durable facts into `MEMORY.md`.

Do not copy temporary debugging noise into `MEMORY.md`.

## Deployment rules

Do not guess deployment information.

If deployment is unknown, write `Unknown`.

If deployment is confirmed, document:

* Server or device name.
* Local path.
* Service name.
* Start command.
* Restart command.
* Stop command.
* Logs command.
* Port.
* Domain.
* Tunnel or reverse proxy.
* Environment file path.
* Backup or rollback process.
* Troubleshooting notes.

## Deepdive rules

Update `DEEPDIVE.md` when discovering:

* Existing routes.
* Existing APIs.
* Important functions.
* Important classes.
* Database structure.
* Config structure.
* Server flow.
* Bot command flow.
* UI page flow.
* Build system.
* Known workarounds.
* Fragile logic.
* Hidden dependencies.
* Platform-specific quirks.

Keep it organized and searchable.

## Multi-platform behavior

This documentation system must work across:

* Zed
* Cursor
* Codex
* Claude Code
* OpenCode
* Devin
* VS Code
* Local terminal agents
* Remote server agents
* Multiple devices

Avoid platform-specific assumptions unless documented.

If a platform has special behavior, document it in `.agents/deepdive.md`.

## Safety boundaries

Do not:

* Delete user files without explicit permission.
* Overwrite existing docs without preserving useful content.
* Invent project facts.
* Invent routes or deployment commands.
* Add secrets, API keys, tokens, cookies, or private keys to docs.
* Treat generated placeholder text as confirmed reality.
* Run destructive commands unless explicitly asked.
* Assume Git exists.
* Skip `CHANGELOG.md`.

## Final response behavior

After working on a project with this skill, respond with:

* What was changed.
* Which files were created or updated.
* Whether `CHANGELOG.md` was updated.
* Whether `HANDOVER.md` needs attention.
* Any missing information the user should fill in.

Keep the final response short unless the user asks for details.
