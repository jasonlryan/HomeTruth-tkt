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

- [x] Invite or cohort code can be validated before signup/onboarding.
- [x] User can enter through a partner cohort and be associated with that cohort after auth.
- [x] Consent screen records the required consent records before partner-linked onboarding proceeds.
- [x] User can set up a property profile during the partner onboarding flow.
- [x] Partner/cohort attribution survives refresh/login transitions.
- [x] Co-branded UI uses configuration/tokens rather than hardcoded Zurich-specific assumptions.
- [x] Ineligible, expired or already-used invite states are handled clearly.
- [x] Analytics events are emitted for invite viewed, consent granted, property started and property completed.
- [x] Verification covers happy path, invalid invite, withdrawn/missing consent and existing-user entry.
- [x] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the co-branded onboarding surface before pilot use. Key decision: standalone HomeTruth-hosted pilot flow versus embedded/white-labelled insurer app flow.

Decision made 2026-05-30:

- Start with a standalone HomeTruth-hosted pilot flow.
- Use partner/cohort configuration for co-branding and copy; do not hardcode Zurich-specific product logic.
- Keep B2C unchanged. Partner onboarding is an optional entry path that adds cohort attribution and consent records to the same user/property model.
- Support two invite modes without a new invite table:
  - cohort code via `partner_cohorts.cohort_key` for broad cohort entry;
  - individual invite code via `cohort_members.external_member_ref` for single-use invite handling.
- Expired state is based on the cohort `end_date`.
- Already-used state applies to individual invite codes once the cohort member is already linked to a user.
- Return to: whether a dedicated `partner_invites` table is needed after pilot mechanics are proven.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-315 for insurer invite and co-branded onboarding.
- Verification: roadmap planning only.
- Notes: should not start before HT-314 consent decisions are reviewed.

### 2026-05-30
- Repo: tickets
- Changed: recorded standalone HomeTruth-hosted pilot flow decision and invite-code semantics.
- Verification: decision reviewed and accepted.
- Notes: no dedicated `partner_invites` table yet; cohort codes and cohort-member external refs cover the first pilot.

### 2026-05-30
- Repo: backend
- Changed:
  - `HomeTruth_BE-staging/services/partnerOnboardingService.js`
  - `HomeTruth_BE-staging/Controllers/partnerOnboardingController.js`
  - `HomeTruth_BE-staging/routes/partnerOnboardingRoutes.js`
  - `HomeTruth_BE-staging/server.js`
- Verification:
  - `node -c` passed for partner onboarding service/controller/route and `server.js`.
  - `git diff --check` passed.
  - Direct local MySQL verification passed for invalid cohort code, expired cohort code, already-used individual invite, valid cohort code, cohort claim after auth, missing required consent rejection, consent capture with withdrawn optional consent, property attach, individual invite claim, used invite rejection and event emission.
  - `npm run db:migrate:status` shows all current migrations up, including `20260530120000-create-partner-cohort-consent.js`.
- Notes: analytics events are emitted through the partner onboarding API and logged structurally for now; durable reporting remains HT-317.

### 2026-05-30
- Repo: frontend
- Changed:
  - `HT_Frontend-staging/src/pages/PartnerOnboarding.jsx`
  - `HT_Frontend-staging/src/api/api.js`
  - `HT_Frontend-staging/src/App.js`
  - `HT_Frontend-staging/src/pages/Login.jsx`
  - `HT_Frontend-staging/src/pages/Register.jsx`
  - `HT_Frontend-staging/src/pages/PropertyProfile.jsx`
- Verification:
  - `npm run build` passed with pre-existing unused-var and Browserslist warnings.
  - `git diff --check` passed.
  - Browser verification passed with mocked APIs for public valid invite, mobile invalid invite, authenticated consent capture and existing-property linking.
  - Token audit of `PartnerOnboarding.jsx` found no hardcoded hex colours, bare Tailwind colour classes, bare radius classes, bare shadows or bold font classes.
- Notes: partner/cohort copy is driven by invite validation response; Zurich appears only as test/mock data, not hardcoded product logic.
