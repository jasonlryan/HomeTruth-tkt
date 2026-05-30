# HT-313: Create property facts and evidence layer

**Priority:** P1
**Repo:** backend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Turn property documents and user inputs into structured `property_facts` backed by `evidence_sources`.

## Description

HomeTruth's insurer value depends on knowing useful things about a property: maintenance dates, risks, certificates, repairs and prevention signals. The schema exists, but the backend does not yet create facts or evidence.

This ticket adds the first controlled fact/evidence creation path. It should support manual/system facts and a narrow set of document-derived facts. AI-created facts must remain `suggested` until confirmed.

## Dependencies

- HT-312: link documents to properties
- HT-308: domain evolution rules

## Expected Files

- `HomeTruth_BE-staging/Controllers/propertyFactController.js`
- `HomeTruth_BE-staging/routes/propertyFactRoutes.js`
- `HomeTruth_BE-staging/services/propertyFactService.js`
- `HomeTruth_BE-staging/services/userDocumentAnalysisService.js`
- `HomeTruth-tickets/open/HT-313-property-facts-and-evidence.md`

## Acceptance Criteria

- [ ] Backend can create a manual or system property fact with optional evidence source.
- [ ] Backend can create an evidence source from a linked property document.
- [ ] AI/document-derived facts are stored with `verification_status = suggested`.
- [ ] Facts preserve `fact_namespace`, `fact_type`, `value_json`, confidence and validity windows.
- [ ] New facts do not overwrite older facts destructively.
- [ ] Property profile can return current facts grouped by namespace/type.
- [ ] Permission checks prevent users from adding facts to properties where they lack permission.
- [ ] Initial fact taxonomy is documented for insurance-relevant MVP facts.
- [ ] Verification covers manual fact creation, evidence-backed fact creation, suggested AI fact creation and fact listing.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the first insurance-relevant fact taxonomy before implementing extraction. Key decision: which facts are first-class for a 500-user insurer pilot versus deferred.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-313 for the property facts/evidence layer.
- Verification: roadmap planning only.
- Notes: uncertain concepts should start here before being promoted to dedicated tables.
