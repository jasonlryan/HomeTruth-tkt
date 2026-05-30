# HT-312: Link documents to properties

**Priority:** P1
**Repo:** backend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Connect the existing user document vault to property profiles through `property_documents`.

## Description

Users can already upload and process documents, but those documents belong to the user rather than to a property. For an insurer pilot, documents must support property records and later evidence/fact extraction.

This ticket adds property context to uploaded documents while preserving the existing document upload pipeline and existing non-property document behaviour.

## Dependencies

- HT-309: property + people database spine
- HT-310: property profile API

## Expected Files

- `HomeTruth_BE-staging/Controllers/userDocumentController.js`
- `HomeTruth_BE-staging/Controllers/propertyRecordController.js`
- `HomeTruth_BE-staging/services/...` document/property linking service
- `HomeTruth_BE-staging/routes/userDocumentRoutes.js`
- `HomeTruth_BE-staging/routes/propertyRecordRoutes.js`
- `HomeTruth-tickets/open/HT-312-link-documents-to-properties.md`

## Acceptance Criteria

- [x] User can link an existing `userDocuments` record to a property they can contribute to.
- [x] Document upload can optionally accept a `propertyId` and create a `property_documents` link.
- [x] Property profile API can list linked documents for that property.
- [x] User cannot link a document they do not own.
- [x] User cannot link a document to a property where they lack permission.
- [x] Existing document upload and chat behaviour remains compatible for non-property documents.
- [x] Duplicate property/document links are prevented.
- [x] No document table consolidation is included.
- [x] Verification covers link, duplicate-link rejection, permission denial and existing upload behaviour.
- [x] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review whether property context is mandatory for insurer cohort users before changing the upload UI. Key decision: optional property linking for general users versus required property linking for pilot users.

## Decision Log / Return To

- 2026-05-30: For HT-312, property linking is optional for general users. The backend should support `propertyId` on upload and explicit existing-document linking, but non-property uploads must continue to work.
- Return to: whether insurer cohort users must upload documents inside a property context. This should be decided in HT-314/HT-315 when cohort membership, consent and invite flow rules exist.
- Return to: whether the frontend should prompt for property selection before upload once HT-312 is available. This belongs in the next frontend document-flow ticket, not this backend ticket.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-312 for document-to-property linking.
- Verification: roadmap planning only.
- Notes: this keeps `userDocuments` intact and adds property context additively.

### 2026-05-30
- Repo: tickets
- Changed: added Decision Log / Return To section for deferred enforcement decisions.
- Verification: ticket scope review.
- Notes: mandatory property-linked uploads for insurer cohorts remains deferred to HT-314/HT-315.

### 2026-05-30
- Repo: backend
- Changed:
  - `HomeTruth_BE-staging/services/propertyDocumentService.js`
  - `HomeTruth_BE-staging/services/propertyRecordService.js`
  - `HomeTruth_BE-staging/Controllers/propertyRecordController.js`
  - `HomeTruth_BE-staging/Controllers/userDocumentController.js`
  - `HomeTruth_BE-staging/routes/propertyRecordRoutes.js`
- Verification:
  - `node -c` passed for changed backend service/controller/route files.
  - `git diff --check` passed.
  - Direct local MySQL verification passed for existing-document link, linked-document listing, property profile `linkedDocuments`, duplicate-link rejection, cross-user document denial, read-only property permission denial, upload without `propertyId`, and upload with `propertyId`.
  - `npm run db:migrate:status` shows baseline and property spine migrations are both up.
- Notes:
  - No schema migration was needed because `property_documents` already exists.
  - Existing `userDocuments` remains the document vault table; `property_documents` adds property context.
