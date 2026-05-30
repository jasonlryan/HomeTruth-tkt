# HT-315: Build insurer invite and co-branded onboarding

**Priority:** P1
**Repo:** both
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Create the invite-led onboarding flow for users introduced by an insurance partner.

## Description

For a 500-person insurer cohort, HomeTruth needs a controlled entry path: invite validation, partner/cohort attribution, consent capture, property setup and handoff into the property profile.

This ticket turns the partner/cohort/consent model into a working user journey. It should support co-branded copy and styling without hardcoding one insurer into the domain model.

## Dependencies

- HT-314: partner cohort and consent model
- HT-311: property profile onboarding UI
- HT-310: property profile API

## Expected Files

- `HomeTruth_BE-staging/routes/partnerOnboardingRoutes.js`
- `HomeTruth_BE-staging/Controllers/partnerOnboardingController.js`
- `HomeTruth_BE-staging/services/partnerOnboardingService.js`
- `HT_Frontend-staging/src/...` invite/onboarding pages
- `HT_Frontend-staging/src/...` partner branding/config integration
- `HomeTruth-tickets/open/HT-315-insurer-invite-onboarding.md`

## Acceptance Criteria

- [ ] Invite or cohort code can be validated before signup/onboarding.
- [ ] User can enter through a partner cohort and be associated with that cohort after auth.
- [ ] Consent screen records the required consent records before partner-linked onboarding proceeds.
- [ ] User can set up a property profile during the partner onboarding flow.
- [ ] Partner/cohort attribution survives refresh/login transitions.
- [ ] Co-branded UI uses configuration/tokens rather than hardcoded Zurich-specific assumptions.
- [ ] Ineligible, expired or already-used invite states are handled clearly.
- [ ] Analytics events are emitted for invite viewed, consent granted, property started and property completed.
- [ ] Verification covers happy path, invalid invite, withdrawn/missing consent and existing-user entry.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the co-branded onboarding surface before pilot use. Key decision: standalone HomeTruth-hosted pilot flow versus embedded/white-labelled insurer app flow.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-315 for insurer invite and co-branded onboarding.
- Verification: roadmap planning only.
- Notes: should not start before HT-314 consent decisions are reviewed.
