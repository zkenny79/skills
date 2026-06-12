# Reference — Migrating Legacy Doc Setups

Load only when a project still carries legacy agent docs:
`CHANGELOG.md` (+`CHANGELOG_ARCHIVE.md`), `CURRENT.md`, `HANDOVER.md`,
`DEEPDIVE.md`, or per-domain topic docs. Goal: the minimal file set from
SKILL.md, with zero unique facts lost.

## Content Mapping

| Legacy | Goes to |
|--------|---------|
| `HANDOVER.md` + old `OVERVIEW.md` | One merged `OVERVIEW.md` — deduplicate, fix stale facts while merging |
| `CURRENT.md` | Durable parts → `MEMORY.md`; the rest → nothing (`git log` covers it) |
| `CHANGELOG.md` / `_ARCHIVE` | Nothing — git history is the record |
| Topic docs (`PAYMENTS.md`, `FRONTEND.md`, …) | Essentials folded into `OVERVIEW.md` sections |
| Deploy history notes | Retroactive annotated `deploy/*` tags |

## Migration Workflow

1. `wc -l` all existing docs; **read them fully** before deciding — stale docs
   still contain unique facts worth keeping.
2. Merge per the mapping table. While merging, verify claims against the code
   and fix stale facts — a wrong reference doc is worse than none.
3. Rewrite `AGENTS.md` to the contract layout (SKILL.md); make `CLAUDE.md`
   the `@AGENTS.md` import. If the old CLAUDE.md had unique rules, fold them
   into AGENTS.md first.
4. Add the detailed-commit-message and deploy-tag rules to `RULES.md`;
   remove all "update changelog/current/handover" duties.
5. Delete legacy files via `git rm` (tell the user git keeps them
   recoverable). Only delete what the user approved.
6. Grep every remaining doc for references to deleted files and fix them
   (read tables, resume instructions, doc indexes).
7. If the current deploy state is known, create retroactive annotated tags:
   `git tag -a deploy/<target>-<yyyymmdd> <commit> -m "<scope>"` and push tags.
8. Report: files deleted/merged, line delta (before/after `wc -l` totals),
   what replaced what, open unknowns.

## Pitfalls

- Old global rules may say "do not rely on git for context recovery" — that
  inverts under this model; update them.
- Legacy docs often reference each other; a missed cross-reference sends
  future agents to a deleted file.
- Keep explicit safety lists verbatim when slimming (gitignore lists, deploy
  exclusion lists) — summarizing them loses enforcement value, and users
  notice.
- Don't delete unnamed files as scope creep: confirm changelogs/archives are
  wanted gone before removing them.
