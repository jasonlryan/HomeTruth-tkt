# HT-314: Model partner cohorts and consent

**Priority:** P1
**Repo:** backend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Add the backend model needed to run a controlled 500-user cohort introduced by an insurance partner.

## Description

An insurer pilot is not just ordinary signup traffic. The platform must know who introduced the user, which cohort they belong to, what consent they granted, and what HomeTruth is allowed to report back.

This ticket creates the partner/cohort/consent foundation before any co-branded onboarding or insurer reporting is built.

## Dependencies

- HT-309: property + people database spine
- HT-308: domain evolution rules

## Expected Files

- `HomeTruth_BE-staging/migrations/...create-partner-cohort-consent.js`
- `HomeTruth_BE-staging/models/partner.js`
- `HomeTruth_BE-staging/models/partnerCohort.js`
- `HomeTruth_BE-staging/models/cohortMember.js`
- `HomeTruth_BE-staging/models/consentRecord.js`
- `HomeTruth_BE-staging/models/index.js`
- `HomeTruth-tickets/open/HT-314-partner-cohort-consent-model.md`

## Acceptance Criteria

- [x] Schema supports a partner organisation, partner cohort and cohort membership.
- [x] Schema supports a consent record with consent type, version, granted/withdrawn status and timestamp.
- [x] Cohort membership can reference a user and optional property after onboarding.
- [x] Partner references avoid storing unnecessary insurer policy PII; external references are opaque where possible.
- [x] Consent scope distinguishes HomeTruth processing from partner reporting.
- [x] Migration is additive and follows HT-308 domain evolution rules.
- [x] Sequelize models and associations are added.
- [x] Migration status is recorded before and after running.
- [x] Verification confirms tables exist and models load.
- [x] Implementation log records changed files and verification performed.

## Review / Decision Gate

Hard review before implementation. Key decision: exact consent scopes and what data Zurich/another insurer is allowed to receive at individual versus aggregate level.

Decision made 2026-05-30:

- Model HomeTruth processing consent separately from partner reporting consent.
- Model partner contact/servicing consent separately from data/reporting consent.
- Individual-level partner report access requires an explicit consent grant.
- Aggregate cohort analytics may be supported only in anonymised/aggregated form.
- Store opaque partner/member references only; do not store unnecessary insurer policy PII in HomeTruth.
- HT-314 creates the schema/model foundation only. Invite UX, branded onboarding and reporting queries remain follow-up work.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-314 for partner cohort and consent modelling.
- Verification: roadmap planning only.
- Notes: this is the main governance checkpoint before insurer-specific work.

### 2026-05-30
- Repo: tickets
- Changed: recorded consent/reporting decision before implementation.
- Verification: decision reviewed and accepted.
- Notes: individual-level partner report access requires explicit consent; aggregate reporting remains anonymised/aggregated only.

### 2026-05-30
- Repo: backend
- Changed:
  - `HomeTruth_BE-staging/migrations/20260530120000-create-partner-cohort-consent.js`
  - `HomeTruth_BE-staging/models/partner.js`
  - `HomeTruth_BE-staging/models/partnerCohort.js`
  - `HomeTruth_BE-staging/models/cohortMember.js`
  - `HomeTruth_BE-staging/models/consentRecord.js`
  - `HomeTruth_BE-staging/models/index.js`
- Migration status before:
  - `up 20260525143000-baseline-existing-schema.js`
  - `up 20260525230000-create-property-people-spine.js`
- Migration run:
  - `npm run db:migrate` applied `20260530120000-create-partner-cohort-consent.js`.
- Migration status after:
  - `up 20260525143000-baseline-existing-schema.js`
  - `up 20260525230000-create-property-people-spine.js`
  - `up 20260530120000-create-partner-cohort-consent.js`
- Verification:
  - `node -c` passed for the migration, new models and `models/index.js`.
  - `git diff --check` passed.
  - Direct local MySQL verification confirmed the four new tables exist, Sequelize models create partner/cohort/member/consent rows, cohort membership can reference user and property, consent records support granted and withdrawn statuses, and model associations load for partner cohorts and member consent records.
- Notes:
  - External partner/member references are opaque strings.
  - No insurer policy number or unnecessary policy PII is stored in the new schema.
