---
name: project-agent-docs-manager
description: Maintain a cross-platform project documentation system for AI agents using AGENTS.md, README.md, and .agents/ folder with deepdive, memory, rules, handover, changelog, deployment, audits, and knowledgebase.
disable-model-invocation: false
---

# Project Agent Docs Manager

Use this skill whenever working on a project that should stay easy to continue across multiple AI agents, devices, editors, platforms, and context compaction.

This skill manages a project documentation system built around:

```text
README.md
AGENTS.md
.agents/
```

The purpose is to make every project self-explaining, even when there is no Git repository, when chat context gets compacted, or when work moves between tools like Zed, Cursor, Codex, Claude Code, OpenCode, Devin, VS Code, or another AI agent platform.

## When to use this skill

Use this skill when the user asks to initialize, maintain, repair, audit, continue, or improve project documentation.

Also use it when the project already contains any of these files:

```text
AGENTS.md
.agents/
.agents/deepdive.md
.agents/memory.md
.agents/rules.md
.agents/handover.md
.agents/changelog.md
.agents/deployment.md
```

Use it before making project changes if the user clearly wants persistent project context, multi-agent workflows, context compaction safety, or no-Git local project continuity.

## Main rule

Before changing code or project files, read the project documentation first.

Default reading order:

```text
README.md
AGENTS.md
.agents/deepdive.md
.agents/rules.md
.agents/memory.md
.agents/handover.md
.agents/changelog.md
.agents/deployment.md
```

If some files do not exist, create them when initializing the docs system.

Never assume Git exists. Never rely on `git status` for context compaction unless the user explicitly asks for Git usage. Prefer `.agents/changelog.md`, `.agents/handover.md`, chat history, `.agents/`, and project files.

## Required documentation structure

At the project root, maintain ONLY:

```text
README.md
AGENTS.md
```

Inside `.agents/`, maintain:

```text
.agents/
── deepdive.md
├── memory.md
├── rules.md
├── handover.md
├── changelog.md
└── deployment.md
```

## File purposes

`README.md` is a short summary. It explains what the project is, what it does, and where to find deeper documentation. Keep it brief and link to AGENTS.md for agent instructions.

`AGENTS.md` is the main instruction file for AI agents. It explains the documentation system, the required reading order, the `.agents/` folder structure, project rules, and how future agents should continue work.

`.agents/deepdive.md` is the extended project knowledge base AND serves as the readme for the `.agents/` folder. It contains:
- Architecture overview
- Important routes, APIs, functions, and modules
- Data flow and server flow
- Existing workarounds and fragile areas
- Known issues
- Implementation details
- Platform-specific quirks
- How to use the `.agents/` folder
- Agent workflow instructions

`.agents/memory.md` stores durable context for context compaction. Include things like "no Git repository", preferred workflows, useful commands, important project facts, known limitations, and long-term conventions. Do not dump every small change here.

`.agents/rules.md` is the strict rulebook. It must include: always use existing routes and conventions, always update `.agents/changelog.md`, never rely on Git status for compaction unless explicitly asked, always check `.agents/changelog.md`, `.agents/handover.md`, chat history, and `.agents/`, do not invent deployment steps, do not overwrite user work without permission.

`.agents/handover.md` stores current in-progress state. It should say what is being worked on, what is unfinished, what needs fixing later, files touched, risks, and next steps. If nothing is unfinished, clearly say that.

`.agents/changelog.md` records every meaningful change. Every change must get a timestamped entry with summary, files changed, reason, and follow-up.

`.agents/deployment.md` documents deployment only when known. Include servers, domains, ports, service names, paths, restart commands, Cloudflare tunnels, Docker, systemd, VPS, Raspberry Pi, environment files, rollback, and troubleshooting. Do not guess.

## Workflow before project changes

1. Read `README.md` and `AGENTS.md`.
2. Read `.agents/deepdive.md` and `.agents/rules.md`.
3. Identify existing routes, files, functions, styles, APIs, components, and conventions.
4. Make the smallest safe change.
6. Update `.agents/changelog.md`.
7. Update `.agents/handover.md` if anything is unfinished or important for the next agent.
8. Update `.agents/memory.md` only if durable long-term context changed.
9. Update `.agents/deepdive.md` only if architecture, routes, functions, workarounds, or deep project knowledge changed.
10. Final response should summarize what changed and which docs were updated.

## Initialization workflow

When initializing this documentation system in a project:

1. Inspect the current project structure.
2. Do not assume Git exists.
3. Create `README.md` (short summary) and `AGENTS.md`.
4. Create `.agents/` structure with all files.
5. Preserve and merge existing documentation instead of overwriting it.
6. Add clear placeholders where project details are unknown.
7. Add the first `.agents/changelog.md` entry.
8. Add a real `.agents/handover.md` status.
9. Tell the user exactly what was created and what still needs filling in.

## Required contents for new files

When creating `README.md`, include:

```markdown
# Project Name

Brief description of what this project is and what it does.

## Documentation

- **Agent instructions**: See [AGENTS.md](./AGENTS.md)
- **Deep project knowledge**: See [.agents/deepdive.md](./.agents/deepdive.md)
- **Current status**: See [.agents/handover.md](./.agents/handover.md)
- **Change history**: See [.agents/changelog.md](./.agents/changelog.md)
```

When creating `AGENTS.md`, include this core instruction:

```markdown
# AGENTS.md

Before making changes, agents must read:

1. README.md
2. AGENTS.md
3. .agents/deepdive.md
4. .agents/rules.md
5. .agents/memory.md
6. .agents/handover.md
7. .agents/changelog.md
8. .agents/deployment.md

Rules:
- Prefer existing routes, files, functions, APIs, components, styles, and conventions.
- Do not assume this project uses Git.
- Do not use Git status as the default context source.
- Always update .agents/changelog.md after meaningful changes.
- Update .agents/handover.md when work is incomplete or current status changes.
- Update .agents/memory.md only for durable long-term context.
- Update .agents/deepdive.md when deep technical knowledge changes.
```

When creating `.agents/deepdive.md`, include:

```markdown
# Deep Project Knowledge

This file contains comprehensive project knowledge and serves as the guide for the .agents/ folder.

## How to use this folder

This folder stores all project documentation for AI agents:

- **deepdive.md**: This file - architecture, routes, APIs, and how to use .agents/
- **memory.md**: Durable context for context compaction
- **rules.md**: Strict project rules and conventions
- **handover.md**: Current work status and unfinished tasks
- **changelog.md**: History of all meaningful changes
- **deployment.md**: Deployment information (servers, ports, commands)

## Agent workflow

1. Read README.md and AGENTS.md at project root.
2. Read this file (deepdive.md).
3. Read .agents/rules.md.
4. Make changes.
5. Update .agents/changelog.md.
6. Update .agents/handover.md if needed.

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

When creating `.agents/rules.md`, include:

```markdown
# Rules

- Always use existing routes, files, functions, APIs, components, styles, and conventions where possible.
- Always document every meaningful change in .agents/changelog.md with a timestamp.
- Keep changelog entries clear and easy to understand.
- For context compaction, never rely on Git repository status unless explicitly asked.
- For context compaction, always check .agents/changelog.md, .agents/handover.md, chat history, and .agents/.
- Do not invent routes, endpoints, commands, configs, deployment paths, or server details.
- Do not delete or overwrite user work without permission.
- After incomplete work, update .agents/handover.md.
```

When creating `.agents/memory.md`, include:

```markdown
# Memory

This file stores durable project context for future agents and context compaction.

## Durable facts

- Git repository: Unknown. Do not assume Git exists.
- Context source priority: .agents/changelog.md, .agents/handover.md, chat history, .agents/, then project files.
- Preferred approach: use existing project routes, files, functions, styles, and conventions before creating new ones.

## Useful techniques

- Before changing code, inspect existing patterns.
- Before deployment changes, check .agents/deployment.md.
- For unfinished work, update .agents/handover.md.
- For every meaningful change, update .agents/changelog.md.
```

When creating `.agents/handover.md`, use:

```markdown
# Handover

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

When creating `.agents/changelog.md`, use newest entries first and this entry format:

```markdown
# Changelog

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

When creating `.agents/deployment.md`, include:

```markdown
# Deployment

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

## Changelog rules

Every meaningful project change must update `.agents/changelog.md`.

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

Update `.agents/handover.md` when:

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

1. `.agents/changelog.md`
2. `.agents/handover.md`
3. Chat history if available
4. `.agents/`
5. `.agents/memory.md`
6. `.agents/deepdive.md`
7. Relevant project files

Summarize only durable facts into `.agents/memory.md`.

Do not copy temporary debugging noise into `.agents/memory.md`.

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

Update `.agents/deepdive.md` when discovering:

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
* Skip `.agents/changelog.md`.

## Final response behavior

After working on a project with this skill, respond with:

* What was changed.
* Which files were created or updated.
* Whether `.agents/changelog.md` was updated.
* Whether `.agents/handover.md` needs attention.
* Any missing information the user should fill in.

Keep the final response short unless the user asks for details.
