# HT-302: Set up Sequelize migrations workflow

**Priority:** P3
**Repo:** backend
**Created:** 2026-03-29
**Updated:** 2026-03-29

## Description

Currently using sync({alter:true}) which auto-modifies tables. This is fine for dev but dangerous for production. Set up sequelize-cli, create initial migration from existing models, establish workflow for future schema changes.

## Files

- `HomeTruth_BE-staging/models/index.js:173` — the sync call
- New `migrations/` directory

## Acceptance Criteria

- [ ] sequelize-cli configured
- [ ] Initial migration exists capturing current schema
- [ ] README documents migration workflow

## Notes

Not urgent for local dev. Important before any schema changes go to production. Discuss with dev team (HT-401).
