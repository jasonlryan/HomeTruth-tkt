# HT-310: Build property profile API

**Priority:** P1
**Repo:** backend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Expose the HT-309 property + people spine through authenticated backend API endpoints so the product can create, list, read and update a user's property profile.

## Description

The database can now store properties, addresses, property-person relationships, documents, evidence and facts. The product cannot yet use that spine because no API layer exists.

This ticket creates the first property profile API surface. It should be intentionally narrow: property identity, current address, current user's relationship, linked-document count and fact summary. It should not implement partner cohorts, document upload changes, evidence extraction or frontend screens.

## Dependencies

- HT-309: property + people database spine
- HT-308: schema contract and domain evolution rules

## Expected Files

- `HomeTruth_BE-staging/routes/propertyRecordRoutes.js`
- `HomeTruth_BE-staging/Controllers/propertyRecordController.js`
- `HomeTruth_BE-staging/services/propertyRecordService.js`
- `HomeTruth_BE-staging/server.js`
- `HomeTruth-tickets/open/HT-310-property-profile-api.md`

## Acceptance Criteria

- [x] Authenticated route group is mounted without conflicting with existing Zoopla `/api/properties` routes.
- [x] Authenticated user can create a property with a current address and explicit `relationshipType`.
- [x] Creating a property also creates the user's `PropertyPerson` relationship.
- [x] Authenticated user can list only properties where they have an active `property_people` relationship.
- [x] Authenticated user can fetch a property profile including current address, their relationship, linked-document count and current fact summary.
- [x] Authenticated user can update property/address fields only when their `permission_level` allows it.
- [x] API returns consistent camelCase JSON while models/tables remain snake_case.
- [x] No data backfill, frontend work, partner/cohort work, or document upload changes are included.
- [x] Verification covers route loading, basic create/list/get/update flow, and permission denial for non-related users.
- [x] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the API contract before starting frontend work. Key decision: final route namespace and permission semantics for `read`, `contribute`, `manage`, and `admin`.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-310 as the first implementation ticket after the property spine.
- Verification: roadmap planning only.
- Notes: this is the immediate next build step.

### 2026-05-30
- Repo: backend
- Changed: added authenticated `/api/property-records` route group, property record controller, and property record service.
- Verification: `node -c` passed for `services/propertyRecordService.js`, `Controllers/propertyRecordController.js`, `routes/propertyRecordRoutes.js`, and `server.js`.
- Notes: route namespace intentionally avoids the existing Zoopla-backed `/api/properties` routes.

### 2026-05-30
- Repo: backend
- Changed: implemented create/list/get/update property profile behavior over the HT-309 property spine.
- Verification: direct service flow against local MySQL created a temporary user/property/address/relationship, listed it, fetched it, updated property/address fields as the admin relationship, denied a related read-only user update with 403, returned 404 for a non-related user, then cleaned up temporary records.
- Notes: creator relationship is `admin`; property/address updates require `manage` or `admin`. `read` can view; `contribute` remains reserved for later document/fact actions.

### 2026-05-30
- Repo: backend
- Changed: API response mapping returns camelCase JSON for property, current address, relationship, linked document count, and current facts.
- Verification: `propertyRecordRoutes` loaded as an Express router and backend `git diff --check` passed.
- Notes: no schema changes, frontend changes, partner/cohort work, document upload changes, or backfill were included.
