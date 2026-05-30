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

- [x] Backend can create a manual or system property fact with optional evidence source.
- [x] Backend can create an evidence source from a linked property document.
- [x] AI/document-derived facts are stored with `verification_status = suggested`.
- [x] Facts preserve `fact_namespace`, `fact_type`, `value_json`, confidence and validity windows.
- [x] New facts do not overwrite older facts destructively.
- [x] Property profile can return current facts grouped by namespace/type.
- [x] Permission checks prevent users from adding facts to properties where they lack permission.
- [x] Initial fact taxonomy is documented for insurance-relevant MVP facts.
- [x] Verification covers manual fact creation, evidence-backed fact creation, suggested AI fact creation and fact listing.
- [x] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the first insurance-relevant fact taxonomy before implementing extraction. Key decision: which facts are first-class for a 500-user insurer pilot versus deferred.

## Decision Log / Return To

- 2026-05-30: First insurer-pilot fact taxonomy is intentionally narrow:
  - `maintenance.last_service_date`
  - `maintenance.next_service_due`
  - `compliance.certificate_expiry`
  - `insurance.policy_expiry`
  - `risk.known_issue`
  - `repair.repair_event`
- 2026-05-30: Manual/system facts may be confirmed; AI/OCR/document-derived facts must start as `suggested`.
- Return to: whether any of these facts deserve dedicated tables after real pilot usage proves lifecycle, workflow or reporting needs.
- Return to: whether one fact needs multiple evidence sources. The first implementation keeps the current single `evidence_source_id` shape.
- Return to: document extraction automation. HT-313 creates controlled fact/evidence APIs and suggested AI fact support, not a broad extractor.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-313 for the property facts/evidence layer.
- Verification: roadmap planning only.
- Notes: uncertain concepts should start here before being promoted to dedicated tables.

### 2026-05-30
- Repo: tickets
- Changed: added Decision Log / Return To section with the initial insurer-pilot fact taxonomy and deferred decisions.
- Verification: ticket scope review.
- Notes: first implementation keeps facts generic and graph-ready; no dedicated insurance/maintenance tables yet.

### 2026-05-30
- Repo: backend
- Changed:
  - `HomeTruth_BE-staging/docs/property-fact-taxonomy.md`
  - `HomeTruth_BE-staging/services/propertyFactService.js`
  - `HomeTruth_BE-staging/Controllers/propertyFactController.js`
  - `HomeTruth_BE-staging/routes/propertyFactRoutes.js`
  - `HomeTruth_BE-staging/routes/propertyRecordRoutes.js`
  - `HomeTruth_BE-staging/services/propertyRecordService.js`
- Verification:
  - `node -c` passed for changed backend service/controller/route files.
  - `git diff --check` passed.
  - Direct local MySQL verification passed for manual fact creation, history preservation, evidence source creation from a linked property document, evidence-backed fact creation, AI-created fact forced to `suggested`, read-only permission denial, grouped fact listing, and property profile grouped fact response.
  - `npm run db:migrate:status` shows baseline and property spine migrations are both up.
- Notes:
  - No schema migration was needed because `evidence_sources` and `property_facts` already exist.
  - Property profile keeps the existing `currentFacts` array and adds `currentFactsByNamespace` for grouped facts.
