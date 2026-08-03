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

- [x] An eligible invite resolves to the correct active programme and campaign context.
- [x] The journey presents approved programme copy while retaining clear HomeTruth identity.
- [x] Required and optional consent scopes are comprehensible, separate and versioned.
- [x] A homeowner can proceed without granting optional partner data access.
- [x] Invalid, expired, paused and closed programme states have safe user-facing behaviour.
- [x] Campaign performance is measurable in aggregate without storing free-text or unnecessary partner PII.
- [x] Browser, API and privacy-boundary tests pass.
- [x] A feature branch, PR and clean review loop are completed.

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

## Delivery Status

Clear to merge as of 2026-08-03. The ticket remains open until both implementation PRs are merged and their merge commits are pulled into the authoritative backend and frontend `main` worktrees.

- Backend: [HomeTruth-be PR #6](https://github.com/jasonlryan/HomeTruth-be/pull/6)
  - base: `06efd28c8acab65a882d6877063c935c2f573d85`
  - head: `2df98e9a14fe7986b083863224f2690faafa05b7`
  - ready, mergeable and `CLEAN`
  - GitGuardian Security Checks passed
- Frontend: [HomeTruth-fe PR #4](https://github.com/jasonlryan/HomeTruth-fe/pull/4)
  - base: `86c9338429a37ccf5b45bf1fe2d507c8d689227f`
  - head: `ccbf484ee5f240e6c357fdf3cb7baa50378a0d06`
  - ready, mergeable and `CLEAN`
  - GitGuardian Security Checks passed

## Implementation Log

### 2026-08-03 — Contract And Documentation

- Recorded the shared-core workstreams, exclusions, consent decisions, attribution boundary and required verification before code changes.
- Added `docs/product/partner-acquisition-consent-contract.md` and linked it from the B2B2C programme scope.
- Documentation commit on `hometruth` main: `34cabfa` (`HT-330: document acquisition consent contract`).
- The contract covers insurer, mortgage-provider, home-developer and other B2B programmes; no insurer-only runtime path was introduced.

### 2026-08-03 — Backend

- Branch: `feature/ht-330-branded-acquisition-consent`.
- Added validated campaign acquisition and consent configuration, canonical scope/version/text-hash derivation and programme-aware invite responses.
- Preserved both cohort-code and individual-invite modes while removing public member, user and property identifiers.
- Made HomeTruth processing the only required scope; all three partner-facing scopes are independent and optional.
- Added atomic consent replacement, stable programme/campaign event attribution and allowlisted acquisition metadata.
- Added public server-controlled invite-view capture, ignored unknown invite telemetry and required processing consent before property start or attachment.
- Added programme/campaign event columns and campaign configuration columns through reversible migration `20260803100000-add-partner-acquisition-consent.js`.
- Added focused verifier `scripts/verifyPartnerAcquisitionJourney.js` and real-MySQL fixture smoke `scripts/smokePartnerAcquisitionJourney.js`.

### 2026-08-03 — Frontend

- Branch: `feature/ht-330-branded-acquisition-consent`.
- Rebuilt the programme landing and onboarding route around approved campaign content, visible HomeTruth identity, privacy boundary, support and safe lifecycle states.
- Added explicit consent choices that all begin off, require an active HomeTruth-processing choice and permit every partner-facing scope to remain declined.
- Removed browser-supplied consent versions and the local consent-complete bypass.
- Limited stored partner context to the invite plus stable programme, campaign and cohort keys.
- Extended operator programme creation with approved acquisition copy, setup expectations, support, branding and consent-version fields.
- Added reusable visual-harness fixtures for all four shared partner types, guest/authenticated states and invalid lifecycle states.
- Made FAQ support accessible to both guest and authenticated homeowners.

## Verification Evidence

### Database And Backend

- Migration status before: `20260803100000-add-partner-acquisition-consent.js` was `down`; all earlier migrations were `up`.
- Applied the migration, verified it `up`, rolled it back, verified it `down`, re-applied it and verified the final status `up` against local MySQL.
- Syntax checks passed for every JavaScript file in the complete backend `main...head` diff.
- Complete backend `git diff --check` passed.
- Focused acquisition contract verifier passed across insurer, mortgage-provider, home-developer and other.
- Existing partner-programme lifecycle verifier passed.
- Existing pilot-reporting coverage verifier passed.
- Real MySQL acquisition smoke passed with fixture cleanup for all four partner types, active programme/campaign resolution, both invite modes, required/optional consent, forged-client version/hash rejection, atomic re-consent, property consent enforcement, public privacy, safe lifecycle states, unknown invite telemetry and programme/campaign attribution.
- Existing partner-programme lifecycle MySQL smoke passed.

### Frontend And Browser

- Focused frontend tests: 2 suites, 8 tests passed.
- Production build passed. It retains two pre-existing unrelated unused-variable warnings in `KnowledgeBaseAdmin.jsx` and `DataPrivacySettings.jsx`, plus the repository's existing Browserslist-age and bundle-size notices.
- Changed-file ESLint passed with no findings.
- Complete frontend `git diff --check` passed.
- Playwright exact-head browser smoke passed for insurer, mortgage-provider, home-developer and other-B2B presentation.
- Guest invitation and authenticated consent passed with every optional permission declined.
- Required-consent error/focus behaviour, safe stored context, guest and authenticated support navigation, invalid/expired/paused/closed states and semantic structure passed.
- The 390px exact-head mobile layout was visually inspected and passed.
- Final journey and support states reported zero console errors.

### Review/Fix Loop

- Review source: clean backend and frontend `main` worktrees at the base SHAs above, using the complete three-dot diff.
- Backend findings fixed:
  - direct property start/attachment did not independently enforce required HomeTruth processing consent;
  - unknown invite codes could create unscoped telemetry rows.
- Frontend findings fixed:
  - downstream property setup still cached member/property identifiers instead of the safe context contract;
  - the configured `/faq` support route redirected authenticated users to the dashboard.
- Regression evidence was added or extended for each relevant boundary.
- Repeated base-to-feature review found no remaining actionable issues.
- Both PRs stayed draft throughout the fix loop and were made ready exactly once after the final local gates passed.

## Remaining Gaps

- HT-319 remains a live-launch blocker for approved withdrawal/deletion policy, identity verification and handling times.
- No target-environment migration, deployment or browser smoke has been performed; those checks must run before production launch.
- HT-331/HT-332 remain responsible for the partner evidence dashboard and governed partner access. HT-330 does not grant partner self-service or individual homeowner data access.
