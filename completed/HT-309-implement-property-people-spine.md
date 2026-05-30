# HT-309: Implement property + people database spine

**Priority:** P1
**Repo:** backend
**Created:** 2026-05-25
**Updated:** 2026-05-30

## Goal

Implement the first HomeTruth property + people database spine defined in HT-308, using explicit Sequelize migrations and models.

This creates the stable backend foundation for:

```text
Property Register + People Experience = HomeTruth
```

## Description

HT-308 defines the schema contract, naming convention, graph-ready constraints, and domain evolution rules. This ticket implements that contract in the backend without destructive data changes or backfills.

The first slice must create the core tables and model associations only. API routes, frontend screens, document upload flow changes, and data backfills are follow-up tickets.

## Dependencies

- HT-307: canonical HomeTruth domain model
- HT-308: property + people database schema contract
- HT-302: Sequelize migration workflow

## Files

- `HomeTruth_BE-staging/README.md` - migration/domain gate
- `HomeTruth_BE-staging/migrations/20260525230000-create-property-people-spine.js` - schema migration
- `HomeTruth_BE-staging/models/property.js` - `Property` model
- `HomeTruth_BE-staging/models/propertyAddress.js` - `PropertyAddress` model
- `HomeTruth_BE-staging/models/propertyPerson.js` - `PropertyPerson` model
- `HomeTruth_BE-staging/models/propertyDocument.js` - `PropertyDocument` model
- `HomeTruth_BE-staging/models/evidenceSource.js` - `EvidenceSource` model
- `HomeTruth_BE-staging/models/propertyFact.js` - `PropertyFact` model
- `HomeTruth_BE-staging/models/index.js` - model imports, associations, exports
- `HomeTruth-tickets/completed/HT-309-implement-property-people-spine.md` - tracking and implementation log

## Acceptance Criteria

- [x] Backend README states that domain schema changes must follow HT-308 and cite the relevant ticket.
- [x] Migration creates `properties`, `property_addresses`, `property_people`, `property_documents`, `evidence_sources`, and `property_facts`.
- [x] Migration is additive only: no destructive changes, no data backfill, and no changes to `users.home_address`, `userDocuments`, `documents`, or `bookmarked_listings`.
- [x] Sequelize models follow HT-308 naming conventions: PascalCase singular model names, explicit snake_case table names, snake_case columns, and `underscored: true`.
- [x] `models/index.js` imports, associates, and exports the new models.
- [x] `npm run db:migrate:status` is recorded before migration.
- [x] `npm run db:migrate` succeeds against local `hometruth-mysql`.
- [x] `npm run db:migrate:status` is recorded after migration.
- [x] Basic model loading verification passes.
- [x] Implementation log records files changed and verification performed.

## Notes

Do not add API routes or frontend changes under this ticket.

Do not backfill existing users or documents under this ticket. Backfill should be a separate ticket after the API and frontend read paths are planned.

Do not introduce a graph database under this ticket. The schema is graph-ready, not graph-first.

## Implementation Log

### 2026-05-25
- Repo: backend / tickets
- Changed: created HT-309 from HT-308 to implement the first additive property + people database spine.
- Verification: ticket created from accepted HT-308 schema contract.
- Notes: implementation must follow HT-308 naming convention and domain evolution rules.

### 2026-05-25
- Repo: backend
- Changed: added the README migration/domain gate requiring domain schema work to follow `docs/property-people-spine-schema.md`, cite tickets, default to additive migrations, preserve compatibility windows, and avoid destructive changes without a deprecation path.
- Verification: `git diff --check` passed in the backend repo.
- Notes: this embeds the HT-308 rule where backend developers see migration instructions.

### 2026-05-25
- Repo: backend
- Changed: added migration `20260525230000-create-property-people-spine.js` creating `properties`, `property_addresses`, `property_people`, `property_documents`, `evidence_sources`, and `property_facts`.
- Verification: `node -c migrations/20260525230000-create-property-people-spine.js` passed.
- Notes: migration is additive only. It does not alter or backfill `users.home_address`, `userDocuments`, `documents`, or `bookmarked_listings`.

### 2026-05-25
- Repo: backend
- Changed: added Sequelize models `Property`, `PropertyAddress`, `PropertyPerson`, `PropertyDocument`, `EvidenceSource`, and `PropertyFact`; updated `models/index.js` with imports, associations, and exports.
- Verification: `node -c` passed for all new model files and `models/index.js`.
- Verification: model loading check passed for `Property`, `PropertyAddress`, `PropertyPerson`, `PropertyDocument`, `EvidenceSource`, and `PropertyFact`.
- Notes: models use explicit `tableName`, snake_case table names, snake_case columns, and `underscored: true` per HT-308.

### 2026-05-25
- Repo: backend
- Verification before migration: `npm run db:migrate:status` showed `up 20260525143000-baseline-existing-schema.js` and `down 20260525230000-create-property-people-spine.js`.
- Verification migration run: `npm run db:migrate` completed successfully; `20260525230000-create-property-people-spine.js` migrated in 0.396s.
- Verification after migration: `npm run db:migrate:status` showed both `20260525143000-baseline-existing-schema.js` and `20260525230000-create-property-people-spine.js` as `up`.
- Verification DB check: direct MySQL table check confirmed `properties`, `property_addresses`, `property_people`, `property_documents`, `evidence_sources`, and `property_facts` exist.
- Notes: local database target was the existing `hometruth` MySQL DB used by the backend migration workflow.

### 2026-05-30
- Repo: tickets
- Changed: closed stale completed ticket as housekeeping after downstream property profile, document linking, facts, partner consent, prevention tasks and pilot analytics were implemented on top of this spine.
- Verification: acceptance criteria were already checked and current migration status includes the property + people spine as `up`.
- Notes: no backend change made under this housekeeping step.
