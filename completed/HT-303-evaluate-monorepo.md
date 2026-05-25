# HT-303: Evaluate monorepo vs separate repos

**Priority:** P4
**Repo:** both
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Consider merging frontend and backend into a single repo for simpler issue
tracking, AI agent access, and a single GitHub Projects board.

Decision: do not merge into a monorepo for now. Keep frontend, backend,
design-system and tickets as separate repositories. Use `HomeTruth-tickets` as
the standalone referenced source of truth for tickets; do not use ticket
submodules or copied ticket trees inside app repos.

## Files

- n/a — decision ticket

## Acceptance Criteria

- [x] Decision made and documented.
- [x] If monorepo: repos merged, or decision recorded not to merge.
- [x] If separate: referenced ticket repo approach documented.

## Notes

Pros: single set of issues, one place for AI agents to look. Cons: harder to merge changes back to team's separate repos later.

Superseded by HT-304, which implemented the simpler separate-repo setup:
frontend/backend repos reference ticket IDs from `HomeTruth-tickets`; they do
not carry ticket submodules.

## Implementation Log

### 2026-05-25

- Repo: tickets
- Changed: closed the decision ticket based on the implemented HT-304 workflow.
- Verification: `HomeTruth-tickets/README.md` documents the standalone
  referenced ticket repo; HT-304 is completed and records removal of frontend
  and backend ticket submodules.
- Notes: keep separate repos unless a future operational need justifies a new
  monorepo evaluation.
