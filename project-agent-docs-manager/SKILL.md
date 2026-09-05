---
name: project-agent-docs-manager
description: Initialize, slim, or migrate agent project docs (AGENTS.md, .agent/). Use when setting up agent documentation, reducing doc token cost, or migrating legacy CHANGELOG/CURRENT/HANDOVER setups to the minimal model.
disable-model-invocation: true
---

# Project Agent Docs Manager

Agent continuity with **minimal token cost**. Git history is the record —
docs carry only what git cannot. Every doc line costs tokens on every future
read, so: few files, all short, read on demand.

Migrating a legacy doc setup (CHANGELOG/CURRENT/HANDOVER/topic docs)?
Follow [reference.md](./reference.md).

## Lean mode (when requested)

For "lean", "minimal", or "abgespeckt", use this mode instead of the full
file set and Init workflow below. Keep the full mode available for other projects.

- Create or trim only the root `AGENTS.md`, targeting 25-45 lines.
- Reuse existing project documentation through a small read-on-demand table.
  Do not create RULES, MEMORY, OVERVIEW, or a new `.agent/` tree by default.
- Keep only verified architecture boundaries, non-obvious invariants, exact
  verification commands, and the user's established change/release policy.
- Get branch and change history from Git. Do not copy a task diary, route catalog,
  current deployment state, or workstation-specific paths into the entry file.
- Preserve an existing CLAUDE import; add one only when requested or already used.
- Put a durable finding beside its existing documentation when possible.
- For a requested cleanup or performance audit, remove duplication only when
  behavior remains covered. Record reproducible before/after measurements;
  don't replace real regression tests with source-text assertions or test counts.
- Report files and line counts. Do not delete existing docs just to meet a budget.

## The File Set

| File | Purpose |
|------|---------|
| `AGENTS.md` (root) | Operating contract (~60–80 lines) |
| `CLAUDE.md` (root) | Thin import only — never divergent content |
| `<docs>/RULES.md` | Short strict rulebook |
| `<docs>/MEMORY.md` | Durable findings in short form (~40 lines) |
| `<docs>/OVERVIEW.md` | The one deep reference for the whole project |
| `<docs>/DEPLOYMENT*.md` | Optional — only if the project deploys |

`<docs>` = existing `.agent/` or `.agents/`; default `.agent/`. **Never**
create CHANGELOG, CURRENT, HANDOVER, DEEPDIVE, or topic docs.

## File Rules

### AGENTS.md — proven layout

1. One-line philosophy: search source directly, smallest safe change, no doc bulk-loading
2. Read-on-demand table with "open only when" per doc:

   | Need | Read |
   |------|------|
   | Changing docs/rules/deploy behavior | `<docs>/RULES.md` |
   | Resume / compaction | `<docs>/MEMORY.md` |
   | Deep context (architecture, settings, APIs) | `<docs>/OVERVIEW.md` |
   | Deployment | `<docs>/DEPLOYMENT.md` |

3. Git section: repo, branch, commit+push policy, never-commit list
4. Project shape: one line per core file/folder
5. Numbered non-negotiables (domain hard rules, security, deploy exclusions)
6. Verification commands + note that compile checks miss runtime errors —
   smoke-test new module-level code via import

**Exclude:** manuals, route catalogs, deploy details — OVERVIEW covers depth.

### CLAUDE.md — exactly this

```markdown
# Claude Entry

Single source of truth — same rules for every agent:

@AGENTS.md
```

### RULES.md

Workflow rules (search first, reuse patterns, verify steps), the
git-as-source-of-truth rule with the explicit gitignore list, the
detailed-commit-message rule (replaces changelog), the deploy-tag rule,
hard domain rules, docs layout list.

### MEMORY.md

Durable findings only: repo/branch + multi-machine workflow, toolchain
gotchas (e.g. minifier quirks), environment quirks, behavior to preserve.
Absolute dates. **Never** recent-change logs — git covers those.

### OVERVIEW.md

The single deep reference: mental model/architecture, env variable names
(never values), DB tables + settings keys, auth/access model, subsystems
with hard constraints, admin/UI map, compact API catalog, command list,
known sharp edges, definition of done. Fix stale facts whenever touching it.

### DEPLOYMENT*.md (optional)

Hosts/targets, transfer method, file exclusion list (secrets, DBs, generated
assets, docs), restart steps, deploy-tag step. No new secrets.

## Conventions That Replace Docs

- **Commit messages** (replace CHANGELOG): precise subject + body with the
  why; one topic per commit; `git log --oneline` must read as feature history
- **History questions:** `git log --grep=...`, `git log -S 'symbol'`
- **Deploy state** (replaces deploy logs): annotated tags
  `deploy/<target>-<yyyymmdd>` (suffix `-2` on same-day repeats);
  `git log deploy/<tag>..HEAD --oneline` = what that server is missing
- **Resume context** (replaces CURRENT): `git log --oneline -20` + MEMORY

## Workflows

**Init:** inspect project → create AGENTS (+ CLAUDE import), RULES, MEMORY,
OVERVIEW; DEPLOYMENT only if deployment exists → unknowns marked `Unknown`.

**Audit:** inspect relevant docs and line counts → report findings with quotations
and concrete proposed edits. An audit alone does not authorize file changes.

**Authorized cleanup:** when the user also requests implementation, edit within
the agreed scope, move depth to existing reference docs, and remove duplication
without losing unique rules. Line targets are guidance, not deletion authority.
Report before/after line counts for changed docs.

**Compaction read order:** AGENTS → MEMORY → `git log --oneline -20` →
OVERVIEW only if fundamentals needed → project files.

## Safety

Deleting existing document files requires explicit user approval. An authorized
documentation edit permits changes to passages within the agreed scope. Reuse
existing explicit approval for the same action and scope instead of asking again.
Merge unique content before deleting its source; verify Git tracks a file before
claiming it is recoverable through Git. No invented facts, paths,
deploy details, or secrets. Preserve `.agent/` vs `.agents/` — never create
a parallel tree.

## Response

For an audit: prioritized findings, quotations, locations, proposed edits, and
any proposed expansion of authority. For implementation: files changed, line
delta, verification, and remaining work. Do not present blocked work as complete.
