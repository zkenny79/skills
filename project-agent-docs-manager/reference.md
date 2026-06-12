# Reference — Project Agent Docs Manager

Load only when applying detailed file rules or full workflows.

## File Rules

### README.md
Short human summary: what, main commands/files, link to docs index. Not the agent brain.

### AGENTS.md
Router + non-negotiables. Include read-on-demand table, project shape, verify commands, deploy pointer.
**Exclude:** long manuals, full changelogs, route/API catalogs, deploy target details.

### CLAUDE.md
Tiny pointer to `AGENTS.md` unless user wants a full separate prompt:

```markdown
# Claude Agent Entry
Read AGENTS.md first.
Key: use docs folder + file scans; no secrets in docs.
```

### RULES.md
Short strict rules + default read policy. Do not duplicate HANDOVER.

### MEMORY.md
Durable facts only: docs folder name, deploy conventions, generated vs source paths, git workflow if confirmed.
No recent debugging noise.

### CURRENT.md
Short active context for compaction/resume. Prune often.

### HANDOVER.md
Deep detail on demand: architecture, routes, settings keys, sharp edges.

### CHANGELOG.md
Recent entries only. Archive to `CHANGELOG_ARCHIVE.md` at ~300–500 lines.
Newest-first; summary + key files + reason; no command transcripts.

### DEPLOYMENT.md
Confirmed deploy only. Exclusions + restart rules. No secrets.

### Topic docs
Add for major domains (e.g. `DISCORD_COMMANDS.md`, `DATABASE.md`) instead of bloating AGENTS.

## Full Maintenance Workflow

1. `find <docs> -name '*.md' | xargs wc -l`
2. Identify oversized always-read files
3. Move long sections from AGENTS → topic docs
4. CLAUDE → pointer unless user wants otherwise
5. RULES must not bulk-load all docs
6. Short-term context → CURRENT
7. Durable facts → MEMORY
8. Old changelog → CHANGELOG_ARCHIVE
9. Update README indexes
10. Report before/after line counts

## Full Init Workflow

1. Inspect project structure
2. Docs folder: existing `.agent/` or `.agents/` wins; else default `.agent/`
3. Create README, AGENTS, optional CLAUDE
4. Create RULES, MEMORY, CURRENT, HANDOVER, CHANGELOG, DEPLOYMENT
5. Topic docs only for obvious major domains
6. Merge existing useful docs — do not blind overwrite
7. Unknown facts → `Unknown`

## Changelog — Meaningful Changes

Code, config, routes/APIs, deploy, doc structure, bugs, refactors, behavior changes.

## Compaction Read Order

1. AGENTS → RULES → CURRENT → MEMORY
2. Relevant topic docs + project files
3. HANDOVER / CHANGELOG / ARCHIVE only if task needs them

## Safety (full)

- No file deletes without explicit permission
- Preserve useful content on overwrite
- No invented facts, routes, commands, paths, servers
- No secrets in docs
- Placeholders ≠ confirmed reality
- No destructive commands unless asked
