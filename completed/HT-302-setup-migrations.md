# HT-302: Set up Sequelize migrations workflow

**Priority:** P3
**Repo:** backend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Goal

Replace implicit runtime schema changes with an explicit Sequelize migration workflow so database changes are deliberate, repeatable, reviewable, and safe for parallel frontend/backend work.

## Description

The backend currently uses `sync({ alter: true })`, which auto-modifies tables when the app starts. This is acceptable for quick local prototyping, but it hides schema changes from review and is unsafe for shared/staging/production databases.

Set up the backend so schema changes are captured in migration files, run via npm scripts, and documented for developers. Keep the first pass non-destructive: migration tooling should be available without forcing an immediate production schema rewrite.

## Files

- `HomeTruth_BE-staging/package.json` — migration scripts and CLI dependency
- `HomeTruth_BE-staging/package-lock.json` — locked CLI dependency tree
- `HomeTruth_BE-staging/.sequelizerc` — Sequelize CLI paths
- `HomeTruth_BE-staging/config/sequelize-cli.js` — CLI database configuration
- `HomeTruth_BE-staging/migrations/` — baseline migration
- `HomeTruth_BE-staging/models/index.js` — runtime sync gate
- `HomeTruth_BE-staging/README.md` — migration runbook

## Acceptance Criteria

- [x] `sequelize-cli` is configured for the backend and reads the existing `.env` / `.env_staging` database settings.
- [x] Backend `package.json` exposes migration scripts for create, run, undo, and status.
- [x] A baseline migration exists to establish the migration history table without altering existing live tables.
- [x] Runtime `db.sync({ alter: true })` is gated behind an explicit local-development flag and is no longer the silent default.
- [x] Backend README documents the migration workflow, including when to create a migration and how to run it locally/staging.
- [x] Ticket implementation log records files changed and verification performed.

## Notes

Not urgent for local dev. Important before any schema changes go to production. Discuss with dev team (HT-401).

## Implementation Log

### 2026-05-25
- Repo: backend
- Changed: added Sequelize CLI configuration, migration npm scripts, a non-destructive baseline migration, and backend README migration workflow documentation. Runtime `db.sync({ alter: true })` now only runs when `AUTO_SYNC_DB=true` is explicitly set.
- Verification: `node -c config/sequelize-cli.js`, `node -c migrations/20260525143000-baseline-existing-schema.js`, `node -c models/index.js`, package JSON parsing, and `git diff --check` passed in `HomeTruth_BE-staging`.
- Verification: initial `npm run db:migrate:status` and `npm run db:migrate` attempts loaded `config/sequelize-cli.js` but failed because local MySQL was not listening at `127.0.0.1:3306`.
- Verification: found stopped Docker container `hometruth-mysql`, started it with `docker start hometruth-mysql`, confirmed port `3306` was listening, reran `npm run db:migrate:status`, ran `npm run db:migrate`, and confirmed final status is `up 20260525143000-baseline-existing-schema.js`.
- Notes: the original backend zip contains Qdrant local vector storage but no MySQL dump, `.sql`, `.sqlite`, or `.db` file. The local relational DB is provided by the Docker container, not by a dump file in the zip. `npm install --save-dev sequelize-cli` reported existing dependency audit findings: 22 vulnerabilities.
