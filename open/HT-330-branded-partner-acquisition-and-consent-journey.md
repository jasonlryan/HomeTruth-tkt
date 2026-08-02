# HT-330: Build branded partner acquisition and consent journey

**Priority:** P1
**Repo:** frontend / backend / docs
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-02

## Goal

Give each partner programme a clear, approved invitation and onboarding route that explains homeowner value and keeps consent choices separate.

## Objective

Make partner attribution, approved co-branding, campaign context and consent versioning work together from invitation through homeowner activation.

## Scope

- Programme-aware landing and invite route.
- Approved partner and HomeTruth copy/assets selected from programme configuration.
- Clear homeowner-first promise, expected setup, privacy boundary and support route.
- Separate HomeTruth processing, aggregate analytics, partner reporting and partner-contact consent choices.
- Aggregate campaign attribution with no unnecessary partner PII.

## Out Of Scope

- Partner-controlled homeowner data sharing.
- Unapproved insurance, credit, claims or property-value claims.
- Email/SMS/CRM delivery integrations before HT-333.

## Acceptance Criteria

- [ ] An eligible invite resolves to the correct active programme and campaign context.
- [ ] The journey presents approved programme copy while retaining clear HomeTruth identity.
- [ ] Required and optional consent scopes are comprehensible, separate and versioned.
- [ ] A homeowner can proceed without granting optional partner data access.
- [ ] Invalid, expired, paused and closed programme states have safe user-facing behaviour.
- [ ] Campaign performance is measurable in aggregate without storing free-text or unnecessary partner PII.
- [ ] Browser, API and privacy-boundary tests pass.
- [ ] A feature branch, PR and clean review loop are completed.

## Dependencies

- HT-328 scope gate accepted.
- HT-329 programme lifecycle administration.
- HT-319 consent withdrawal and deletion decisions for live launch.
