# Reference — Project Agent Docs Manager

Load only when applying detailed file rules or full workflows.

## File Rules

### AGENTS.md (root, ~60–80 lines)
The operating contract. Structure (proven layout):

1. One-line philosophy: search source directly, smallest safe change, no doc bulk-loading
2. Read-on-demand table (RULES / MEMORY / OVERVIEW / DEPLOYMENT with "open only when")
3. Git section: repo, branch, commit+push policy, never-commit list
4. Project shape: one line per core file/folder
5. Numbered non-negotiables (domain hard rules, security, deploy exclusions)
6. Verification commands (+ note that compile checks miss runtime errors — smoke-test imports)

**Exclude:** manuals, route catalogs, deploy target details, anything OVERVIEW covers.

### CLAUDE.md (root)
Exactly this — never independent content:

```markdown
# Claude Entry

Single source of truth — same rules for every agent:

@AGENTS.md
```

### RULES.md
Short strict rulebook agents load when changing docs/rules/deploy behavior:
workflow rules (search first, reuse patterns, rebuild/verify steps), the
git-as-source-of-truth rule with the explicit gitignore list, the
detailed-commit-message rule (replaces changelog), the deploy-tag rule
(`deploy/<target>-<yyyymmdd>`, annotated, `-2` on same-day repeats), hard
domain rules, and the docs layout list.

### MEMORY.md (~40 lines)
Durable findings only, short form: repo/branch + multi-machine workflow,
build/toolchain gotchas (e.g. minifier quirks), environment quirks (e.g. cloud
sync conflict-renames), behavior that must be preserved. Convert relative dates
to absolute. **Never** recent-change logs — git covers those.

### OVERVIEW.md (the one deep reference)
Merged former overview+handover content, deduplicated: mental model /
architecture, env variable names (never values), DB tables + settings keys,
auth/access model, domain subsystems with their hard constraints, admin/UI map,
API catalog (compact tables), CLI/command list, known sharp edges, definition
of done. Fix stale facts whenever touching it — a wrong reference doc is worse
than none.

### DEPLOYMENT.md / DEPLOYMENT_<VARIANT>.md (optional)
Only for projects that deploy: hosts/targets, transfer method, file exclusion
list (secrets, DBs, generated assets, docs), restart steps, and the deploy-tag
step (`git tag -a deploy/<target>-<yyyymmdd> <commit> -m "<scope>"` +
`git push origin --tags`). No secrets beyond what the user already stored here
knowingly.

## Migration Workflow (legacy → minimal)

1. `wc -l` all existing docs; read them fully before deciding
2. Map content: HANDOVER+OVERVIEW → new OVERVIEW (merge, dedupe, fix stale
   facts); CURRENT/MEMORY → new MEMORY (durable only); CHANGELOG → nothing
   (git history); topic docs → fold essentials into OVERVIEW
3. Rewrite AGENTS.md to the contract layout; make CLAUDE.md the `@AGENTS.md` import
4. Add commit-message + deploy-tag rules to RULES.md
5. `git rm` legacy files (CURRENT, HANDOVER, CHANGELOG(+ARCHIVE), topic docs)
   — note for the user that git keeps them recoverable
6. Grep all remaining docs for references to deleted files and fix them
7. If deploy state is known, create retroactive annotated `deploy/*` tags
8. Report: files deleted/merged, line delta, what replaced what

## Conventions That Replace Docs

- **Commit messages:** precise subject + body with the why; one topic per
  commit; `git log --oneline` must read as the feature history
- **History questions:** `git log --grep=...`, `git log -S 'symbol'`
- **Deploy state:** annotated tags `deploy/<target>-<yyyymmdd>`;
  `git log deploy/<tag>..HEAD --oneline` = what that server is missing

## Compaction Read Order

1. AGENTS.md → MEMORY.md → `git log --oneline -20`
2. OVERVIEW.md only if fundamentals are needed
3. Project files

## Safety (full)

- Delete only with user approval; mention git recoverability
- Merge unique content before deleting its source
- No invented facts, routes, commands, paths, or servers
- No secrets in docs; placeholders ≠ confirmed reality
- Preserve `.agent/` vs `.agents/` — never create a parallel tree
