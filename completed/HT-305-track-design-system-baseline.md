# HT-305: Track canonical design-system baseline

**Priority:** P1
**Repo:** design-system
**Created:** 2026-05-25
**Updated:** 2026-05-25

## Goal

Make `design-system/` a version-controlled source of truth so HomeTruth brand,
token, component, logo and voice decisions are auditable before they are
implemented in frontend or backend work.

## Description

The design-system folder currently exists as a top-level workspace folder, but
it is not inside a Git repo. That means design-system changes cannot yet be
committed, reviewed, or reliably briefed back to the team.

Before frontend Tailwind or component migration starts, capture the current
design-system state as a tracked baseline and document the governance rule that
design-system changes require both a ticket implementation log and changelog
entry.

## Files

- `design-system/.gitignore` — ignore local machine files
- `design-system/design-system.md` — governance and source-of-truth rules
- `design-system/CHANGELOG.md` — baseline changelog
- `design-system/tokens/` — canonical token source
- `design-system/foundations/` — foundation documentation
- `design-system/components/` — component spec scaffold

## Acceptance Criteria

- [x] `design-system/` is initialised as its own Git repo.
- [x] Current design-system files are committed as a baseline with `HT-305` in the commit message.
- [x] Local-only files such as `.DS_Store` are ignored.
- [x] Governance states that design-system changes require a ticket implementation log and changelog update.
- [x] The implementation log records the baseline commit and any follow-up risks.

## Implementation Log

### 2026-05-25

- Repo: design-system
- Changed: initialised `design-system/` as a standalone Git repo, added
  `.gitignore`, and committed the current design-system files as the baseline.
- Verification: baseline commit created successfully:
  `933edf7 HT-305: track design-system baseline`.
- Notes: no remote is configured yet for the design-system repo. The team still
  needs to decide whether this becomes its own remote repo or is later moved
  into a wider workspace/monorepo.
