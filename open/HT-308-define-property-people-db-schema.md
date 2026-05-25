# HT-308: Define property + people database schema

**Priority:** P1
**Repo:** backend
**Created:** 2026-05-25
**Updated:** 2026-05-25

## Goal

Translate the reviewed HomeTruth domain model into a database-only schema contract for the first property register + people experience spine, without applying migrations yet.

The first schema slice should make the backend ready to model:

```text
Property Register + People Experience = HomeTruth
```

## Description

HT-307 defines the canonical domain language. This ticket turns that model into an implementation-ready MySQL / Sequelize schema specification before any table is created.

The schema must be graph-ready but not graph-first: relational MySQL remains the source of truth, while table names, relationship tables, facts, evidence, provenance, confidence, and validity windows are structured so they can later be projected into a knowledge graph.

## Files

- `HomeTruth_BE-staging/docs/property-people-spine-schema.md` - backend schema contract
- `HomeTruth_BE-staging/docs/property-people-spine-erd.html` - visual HTML ERD reference
- `HomeTruth-tickets/open/HT-308-define-property-people-db-schema.md` - tracking and implementation log

## Acceptance Criteria

- [x] Schema spec defines the first backend spine tables: `properties`, `property_addresses`, `property_people`, `property_documents`, `evidence_sources`, and `property_facts`.
- [x] Each table has a clear purpose, core columns, relationships, indexes, and implementation notes.
- [x] Schema spec preserves the property + people concept from HT-307.
- [x] Schema spec records graph-ready requirements for relationships, facts, evidence, provenance, confidence, and time windows.
- [x] Schema spec defines naming conventions across domain language, MySQL tables/columns, Sequelize models/files, and API JSON.
- [x] Schema spec records domain evolution rules so future expansion is additive, ticketed, and compatible.
- [x] Schema spec explains how existing backend data maps into the new schema without destructive migration.
- [x] Schema spec explicitly defers migrations, APIs, blockchain, marketplace, enterprise pulls, and psychographic matching.
- [x] HTML ERD reference shows the table connections using the HomeTruth design-system tokens and assets.
- [x] Schema spec is reviewed and accepted before HT-309 migration work begins.

## Notes

Do not create or run migrations under this ticket. HT-308 is the schema contract. HT-309 should implement the accepted migration and model layer.

Prefer `property_people` as the table name for the relationship spine. The current backend only has authenticated `users`, so the first implementation can reference `users.id`, but the domain language must stay broad enough for people connected to a property in different roles.

## Implementation Log

### 2026-05-25
- Repo: backend / tickets
- Changed: created HT-308 and added the backend schema contract for the property + people spine.
- Verification: checked the current backend model shape for `users`, `userDocuments`, `documents`, and `bookmarked_listings`; aligned schema spec with HT-307 domain model and live migration workflow from HT-302.
- Notes: no migration was created or run. Existing upload pipeline remains based on `userDocuments`; the first schema slice links property records to those uploaded documents rather than replacing the document vault immediately.

### 2026-05-25
- Repo: backend / tickets
- Changed: added a visual HTML ERD reference for the property + people spine, using HomeTruth design-system tokens, logo assets, and Gill Sans webfonts.
- Verification: HTML reference checked for local design-token and asset links, ASCII-only content, and whitespace via backend/tickets diff checks.
- Notes: this is documentation only. It does not alter migrations, Sequelize models, API routes, or frontend screens.

### 2026-05-25
- Repo: backend / tickets
- Changed: adjusted the HTML ERD reference to avoid bold Gill Sans usage. Removed the bold webfont load and changed labels, pills, table headers, keys, and strong text to regular weight.
- Verification: checked the HTML for remaining bold font-weight usage and reran backend/tickets diff checks.
- Notes: design-system tokens were not changed; this is a local reference-page adjustment before any design-system typography decision is made.

### 2026-05-25
- Repo: backend / tickets
- Changed: added explicit naming conventions to the schema contract: PascalCase singular domain/model names, snake_case plural MySQL table names, snake_case columns, and camelCase API JSON fields.
- Verification: reviewed the convention against current backend naming drift and reran backend/tickets diff checks.
- Notes: HT-309 should map models such as `PropertyPerson` to tables such as `property_people` using explicit Sequelize `tableName` and `underscored: true`.

### 2026-05-25
- Repo: backend / tickets
- Changed: added domain evolution rules to the schema contract so HT-308 is treated as a stable first spine, not a final schema.
- Verification: reviewed the rules against the current requirement to keep expanding the domain model without breaking existing code, data, or team understanding.
- Notes: this is captured in repo documentation and ticket source of truth first. A Codex skill can mirror the behavior later, but the project rule belongs in version-controlled docs.

### 2026-05-25
- Repo: tickets
- Changed: marked HT-308 schema spec as reviewed and accepted for HT-309 implementation.
- Verification: user approved proceeding after the naming convention and domain evolution rules were captured.
- Notes: acceptance applies to the first stable schema spine, not a final exhaustive domain model.
