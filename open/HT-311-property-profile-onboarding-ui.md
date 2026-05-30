# HT-311: Build property profile onboarding UI

**Priority:** P1
**Repo:** frontend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Create the first user-facing flow that lets an authenticated HomeTruth user create or claim a property profile using the HT-310 API.

## Description

HomeTruth needs a visible product experience for the property + people model. This ticket creates the property onboarding/profile UI for a normal authenticated user before insurer-specific cohort flows are added.

The UI should be simple, operational and design-system compliant. It should get a user from "I have no property profile" to "I can see my property, address, relationship and next required actions."

## Dependencies

- HT-310: property profile API
- HT-306: design tokens wired into frontend
- HT-308: domain evolution rules

## Expected Files

- `HT_Frontend-staging/src/...` property profile/onboarding page and components
- `HT_Frontend-staging/src/...` API client helpers if present in existing patterns
- `HomeTruth-tickets/open/HT-311-property-profile-onboarding-ui.md`

## Acceptance Criteria

- [ ] Authenticated user with no property profile sees a property onboarding flow.
- [ ] User can enter address fields and choose an explicit relationship type.
- [ ] UI calls HT-310 create endpoint and handles success/failure states.
- [ ] User with a property profile sees a profile summary with current address and their relationship.
- [ ] UI shows placeholders for documents, facts and next actions without inventing unsupported backend data.
- [ ] UI uses HomeTruth design-system tokens and avoids hardcoded colours/type decisions.
- [ ] Mobile and desktop layouts are usable and text does not overlap.
- [ ] No insurer-specific branding, cohort logic or consent logic is included yet.
- [ ] Verification includes browser check of onboarding and existing-property states.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the first property profile UX before adding insurer-specific onboarding. Key decision: whether the user-facing language says "claim", "create", or "set up" a property.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-311 for the first frontend property profile/onboarding flow.
- Verification: roadmap planning only.
- Notes: depends on HT-310 API contract.
