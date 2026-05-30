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

- [ ] Authenticated route group is mounted without conflicting with existing Zoopla `/api/properties` routes.
- [ ] Authenticated user can create a property with a current address and explicit `relationshipType`.
- [ ] Creating a property also creates the user's `PropertyPerson` relationship.
- [ ] Authenticated user can list only properties where they have an active `property_people` relationship.
- [ ] Authenticated user can fetch a property profile including current address, their relationship, linked-document count and current fact summary.
- [ ] Authenticated user can update property/address fields only when their `permission_level` allows it.
- [ ] API returns consistent camelCase JSON while models/tables remain snake_case.
- [ ] No data backfill, frontend work, partner/cohort work, or document upload changes are included.
- [ ] Verification covers route loading, basic create/list/get/update flow, and permission denial for non-related users.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the API contract before starting frontend work. Key decision: final route namespace and permission semantics for `read`, `contribute`, `manage`, and `admin`.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-310 as the first implementation ticket after the property spine.
- Verification: roadmap planning only.
- Notes: this is the immediate next build step.
