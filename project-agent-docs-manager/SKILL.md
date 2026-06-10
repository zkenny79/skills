---
name: project-agent-docs-manager
description: Maintain token-efficient project documentation for AI agents using compact AGENTS.md/CLAUDE.md entry files plus read-on-demand .agent or .agents docs for memory, rules, current context, handover, changelog, deployment, audits, and knowledgebase.
disable-model-invocation: false
---

# Project Agent Docs Manager

Use this skill when the user asks to initialize, maintain, repair, audit, or
reduce token usage in project docs for AI agents across Codex, Claude Code,
Cursor, Zed, OpenCode, Devin, VS Code, local terminal agents, or context
compaction.

The goal is continuity with low default token cost.

## Core Principle

Do not make every agent read every project doc.

Use progressive disclosure:

1. Tiny always-read entry docs.
2. Short current/memory docs for compaction and resume.
3. Topic docs loaded only when the task touches that topic.
4. Deep handover/archive docs loaded only when needed.

## Detect Existing Layout

Before editing docs:

1. Check for `AGENTS.md`, `CLAUDE.md`, `README.md`.
2. Check for `.agent/` and `.agents/`.
3. Prefer the existing docs folder. If `.agent/` exists, keep using `.agent/`.
   If `.agents/` exists, keep using `.agents/`.
4. Do not create a parallel `.agent/`/`.agents/` tree unless the user explicitly
   asks for migration.
5. Never assume Git exists. Use docs, chat history, direct file scans, and current
   files as context sources.

## Token-Saving Target Structure

At project root:

```text
README.md      short human/project summary
AGENTS.md      compact agent router + non-negotiables
CLAUDE.md      tiny pointer to AGENTS.md, if Claude needs a separate file
```

Inside the chosen docs folder (`.agent/` or `.agents/`):

```text
RULES.md              short strict rulebook
MEMORY.md             durable facts only
CURRENT.md            short active context/recent behavior
HANDOVER.md           deep technical handover, read on demand
CHANGELOG.md          short recent changelog
CHANGELOG_ARCHIVE.md  older history, read rarely
DEPLOYMENT.md         confirmed deploy rules
DEPLOYMENT_REBRANDS.md optional extra target rules
audits/               optional review notes
knowledgebase/        optional durable external/project knowledge
```

For large projects, add topic docs instead of bloating `AGENTS.md`:

```text
RESTORE_VERIFY.md
PAYMENTS_DELIVERY.md
FRONTEND_NOTIFICATIONS.md
DISCORD_COMMANDS.md
DATABASE.md
```

Only create topic docs that are actually useful for that project.

## Default Reading Policy

`AGENTS.md` should tell agents to always read only:

```text
AGENTS.md
<docs>/RULES.md
```

Then read conditionally:

- Resume/compaction: `<docs>/MEMORY.md` and `<docs>/CURRENT.md`
- Recent behavior/regressions: `<docs>/CURRENT.md`, then `<docs>/CHANGELOG.md`
- Deep implementation detail: `<docs>/HANDOVER.md`
- Deployment: `<docs>/DEPLOYMENT.md` or target-specific deployment docs
- Topic work: matching topic doc only
- Older history: `<docs>/CHANGELOG_ARCHIVE.md` only when explicitly useful

Avoid wording that forces agents to read `HANDOVER.md` and the full changelog for
small tasks.

## File Rules

### README.md

Keep it short. It should explain what the project is, main files/commands, and
link to the docs index. Do not make it the agent brain.

### AGENTS.md

Keep it compact, ideally under 150-250 lines.

Include:

- Docs router/read-on-demand table.
- No-Git/source-of-truth rule.
- Project shape.
- Non-negotiables.
- Verification commands.
- Deployment pointer only.

Do not embed long domain manuals, full changelogs, route catalogs, API catalogs,
or deployment target details unless tiny.

### CLAUDE.md

Make it a tiny pointer unless the user explicitly wants a separate full Claude
prompt.

Good pattern:

```markdown
# Claude Agent Entry

Read AGENTS.md first. It is the authority for this project.

Key reminders:
- This workspace has no local Git/source-control metadata.
- Use direct file scans and the docs folder as source of truth.
- Do not deploy secrets, DB files, generated assets, or agent docs unless asked.
```

### RULES.md

Short strict rules. Include the default reading policy and non-negotiables. Do
not duplicate `HANDOVER.md`.

### MEMORY.md

Durable facts only. Good examples:

- no Git/source-control metadata
- chosen docs folder name
- critical deployment convention
- generated-vs-source folders

Do not store every recent change or debugging noise here.

### CURRENT.md

Short active context for compaction/resume. Keep it small and prune it. Use it
for behavior future agents are likely to need soon.

### HANDOVER.md

Deep technical handover. Keep route catalogs, settings keys, architecture, sharp
edges, and implementation detail here. It is read on demand, not by default.

### CHANGELOG.md

Keep recent entries only. If it grows large, split older entries to
`CHANGELOG_ARCHIVE.md`.

Recommended threshold: archive once `CHANGELOG.md` exceeds roughly 300-500 lines
or becomes costly to scan.

### DEPLOYMENT.md

Document confirmed deployment only. Do not guess. Include exclusions and restart
rules. Never store passwords/secrets.

## Maintenance Workflow

When improving an existing docs system:

1. Count markdown file sizes with `find ... -name '*.md' | xargs wc -l`.
2. Identify always-read files that are too large.
3. Move long domain sections out of `AGENTS.md` into topic docs.
4. Make `CLAUDE.md` a pointer unless the user wants otherwise.
5. Update `RULES.md` so it does not require bulk-loading all docs.
6. Move short-term active context to `CURRENT.md`.
7. Keep durable facts in `MEMORY.md`.
8. Split old changelog entries to `CHANGELOG_ARCHIVE.md` when useful.
9. Update README/doc indexes.
10. Report before/after line counts and changed files.

## Initialization Workflow

When initializing from scratch:

1. Inspect the project structure.
2. Ask or infer the docs folder name; default to `.agent/` only if no existing
   convention exists.
3. Create compact `README.md`, `AGENTS.md`, and optional `CLAUDE.md`.
4. Create `RULES.md`, `MEMORY.md`, `CURRENT.md`, `HANDOVER.md`,
   `CHANGELOG.md`, and `DEPLOYMENT.md` in the docs folder.
5. Add topic docs only for obvious major domains.
6. Preserve and merge existing useful documentation instead of overwriting it.
7. Add placeholders only where facts are unknown, clearly marked `Unknown`.

## Changelog Policy

Record meaningful changes, but keep entries concise.

Meaningful changes include:

- Code edits
- Config edits
- Route/API changes
- Deployment changes
- Documentation structure changes
- Bug fixes
- Refactors
- New or removed behavior

Use newest-first entries. Include summary, files changed when useful, reason, and
follow-up only when it adds value. Avoid verbose per-command transcripts.

## Context Compaction Policy

For compaction/resume, do not check Git by default.

Use:

1. `AGENTS.md`
2. `<docs>/RULES.md`
3. `<docs>/CURRENT.md`
4. `<docs>/MEMORY.md`
5. Relevant topic docs
6. Relevant project files

Only load `HANDOVER.md`, `CHANGELOG.md`, or `CHANGELOG_ARCHIVE.md` if needed for
the task.

## Safety Boundaries

Do not:

- Delete user files without explicit permission.
- Overwrite existing docs without preserving useful content.
- Invent project facts, routes, commands, deployment paths, or server details.
- Add secrets, API keys, tokens, cookies, passwords, or private keys to docs.
- Treat generated placeholder text as confirmed reality.
- Run destructive commands unless explicitly asked.
- Assume Git/source-control metadata exists.

## Final Response

Keep it short:

- What changed.
- Which docs were updated.
- Whether the default token path got smaller.
- Any docs still needing user-specific facts.
