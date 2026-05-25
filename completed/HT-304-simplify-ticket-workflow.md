# HT-304: Simplify ticket workflow to standalone referenced repo

**Priority:** P1
**Repo:** both
**Created:** 2026-05-25
**Updated:** 2026-05-25

## Goal

Make `HomeTruth-tickets` the only ticket workspace, with frontend and backend
referencing ticket IDs instead of carrying ticket submodules or copied ticket
trees.

## Description

Remove the ticket submodules from the frontend and backend repos. Keep
`HomeTruth-tickets` as the single ticket source of truth and reference ticket
IDs from frontend, backend, design-system, branches, commits and pull requests.

## Files

- `HT_Frontend-staging/.gitmodules` — remove submodule config
- `HT_Frontend-staging/HomeTruth-tkt` — remove submodule pointer
- `HT_Frontend-staging/README.md` — document ticket workflow
- `HT_Frontend-staging/package.json` — remove stale `sync:tickets` script
- `HomeTruth_BE-staging/.gitmodules` — remove submodule config
- `HomeTruth_BE-staging/HomeTruth-tkt` — remove submodule pointer
- `HomeTruth_BE-staging/README.md` — document ticket workflow
- `HomeTruth_BE-staging/package.json` — remove stale `sync:tickets` script
- `HomeTruth-tickets/README.md` — document ways of working
- `HomeTruth-tickets/.gitignore` — ignore `.DS_Store`

## Acceptance Criteria

- [x] Frontend no longer contains a `HomeTruth-tkt` submodule.
- [x] Backend no longer contains a `HomeTruth-tkt` submodule.
- [x] No app repo references `sync:tickets` or `sync-tickets`.
- [x] Ticket repo README states the traceability rule for all changes.
- [x] Frontend/backend docs point contributors to `../HomeTruth-tickets`.

## Implementation Log

### 2026-05-25

- Repo: both
- Changed: removed ticket submodule wiring from frontend and backend, removed
  stale ticket sync npm scripts, added ticket workflow docs, and added a
  `.DS_Store` ignore rule to the ticket repo.
- Verification: checked Git no longer reports submodules, searched app repos for
  `HomeTruth-tkt`, `sync:tickets`, and `sync-tickets`, and parsed both app
  `package.json` files.
- Notes: ticket updates now happen only in `HomeTruth-tickets`; app repos should
  reference ticket IDs rather than carrying a checkout.
