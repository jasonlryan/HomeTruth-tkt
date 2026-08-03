# HT-330: Build branded partner acquisition and consent journey

**Priority:** P1
**Repo:** frontend / backend / docs
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-03

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
- Partner self-service configuration, governed partner roles or a partner reporting dashboard.
- Enabling individual homeowner report access in the acquisition journey.

## Implementation Workstreams

1. **Approved acquisition contract:** add shared programme/campaign configuration for approved homeowner copy, partner asset references, support route and a versioned consent contract without embedding vertical-specific logic.
2. **Programme-aware invite resolution:** return only the active programme and campaign context attached to the eligible cohort/member, with safe invalid, expired, paused and closed responses.
3. **Consent integrity:** derive consent version, scope requirements and text hashes from server-controlled programme configuration; require HomeTruth processing only and let the homeowner decline every optional partner-facing scope.
4. **Aggregate attribution:** attach stable programme and campaign identifiers to acquisition events and restrict onboarding metadata to an approved structured allowlist rather than free text or partner PII.
5. **Homeowner journey:** present HomeTruth identity, approved co-branding, homeowner value, expected setup, privacy boundary, support route and separate accessible consent choices across unauthenticated and authenticated states.
6. **Compatibility and privacy:** preserve existing cohort and individual invite modes, existing membership/consent records and property handoff while preventing public responses from exposing member, user or property identifiers.

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

## Review Gate

Decision recorded 2026-08-03:

- Build the shared, HomeTruth-hosted acquisition and consent journey now on the merged HT-329 lifecycle; do not wait for a named insurer or introduce a vertical-specific route.
- HomeTruth processing is the only required onboarding consent. Aggregate analytics, aggregate partner reporting and partner contact/servicing are separate optional choices and must default off.
- Do not offer or infer individual report access in HT-330. That requires the later governed-access path and a separate explicit product decision.
- The active programme/campaign configuration is authoritative for copy, assets, support information, consent version and consent text. The browser must not supply or override the authoritative version or hash.
- HT-319 remains a live-launch governance dependency. Its unresolved legal/privacy approval, identity-verification and deletion-policy decisions do not block building or testing the non-destructive technical journey, but they must remain an explicit launch gap.
- Campaign attribution stores stable internal programme/campaign identifiers and allowlisted categorical metadata only. It must not store arbitrary browser-provided free text, policy numbers, mortgage references, purchaser data or contact details.

## Required Verification

- Record migration status before and after applying any HT-330 schema change; verify rollback and re-apply against local MySQL.
- Run syntax checks for every changed backend JavaScript file and `git diff --check` in each implementation repository.
- Add a focused acquisition/consent verifier covering all four shared partner types, active programme/campaign resolution, both invite modes, required-versus-optional consent, server-derived version/hash evidence, safe invalid lifecycle states, public response privacy and allowlisted campaign attribution.
- Run the existing partner-programme lifecycle and pilot-reporting verifiers to protect HT-329 and earlier pilot compatibility.
- Run a real local MySQL smoke with fixture cleanup for programme-aware invite validation, consent recording and campaign attribution.
- Add focused frontend tests for configured acquisition content, consent defaults/payload, safe status presentation and stored-context compatibility.
- Run the frontend production build and changed-file lint.
- Browser-smoke the exact frontend feature head for insurer, mortgage-provider, home-developer and other-B2B presentation; unauthenticated invitation; authenticated consent with every optional scope declined; invalid/expired/paused/closed states; support route; accessibility; and narrow/mobile layout.
- Complete the base-branch review/fix loop and record PR URLs, base/head SHAs, final local gates, CI, mergeability and target-environment or HT-319 launch gaps before closure.
