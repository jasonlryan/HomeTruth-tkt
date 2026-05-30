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

- [ ] Schema supports a partner organisation, partner cohort and cohort membership.
- [ ] Schema supports a consent record with consent type, version, granted/withdrawn status and timestamp.
- [ ] Cohort membership can reference a user and optional property after onboarding.
- [ ] Partner references avoid storing unnecessary insurer policy PII; external references are opaque where possible.
- [ ] Consent scope distinguishes HomeTruth processing from partner reporting.
- [ ] Migration is additive and follows HT-308 domain evolution rules.
- [ ] Sequelize models and associations are added.
- [ ] Migration status is recorded before and after running.
- [ ] Verification confirms tables exist and models load.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Hard review before implementation. Key decision: exact consent scopes and what data Zurich/another insurer is allowed to receive at individual versus aggregate level.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-314 for partner cohort and consent modelling.
- Verification: roadmap planning only.
- Notes: this is the main governance checkpoint before insurer-specific work.
