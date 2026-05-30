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

- [ ] User can link an existing `userDocuments` record to a property they can contribute to.
- [ ] Document upload can optionally accept a `propertyId` and create a `property_documents` link.
- [ ] Property profile API can list linked documents for that property.
- [ ] User cannot link a document they do not own.
- [ ] User cannot link a document to a property where they lack permission.
- [ ] Existing document upload and chat behaviour remains compatible for non-property documents.
- [ ] Duplicate property/document links are prevented.
- [ ] No document table consolidation is included.
- [ ] Verification covers link, duplicate-link rejection, permission denial and existing upload behaviour.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review whether property context is mandatory for insurer cohort users before changing the upload UI. Key decision: optional property linking for general users versus required property linking for pilot users.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-312 for document-to-property linking.
- Verification: roadmap planning only.
- Notes: this keeps `userDocuments` intact and adds property context additively.
