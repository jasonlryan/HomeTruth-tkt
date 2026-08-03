# HT-332: Add governed partner access and audit controls

**Priority:** P1
**Repo:** backend / frontend / docs
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-03

## Goal

Provide the minimum role, access and audit model required for a partner to use programme capabilities without exposing homeowner data.

## Objective

Define and enforce partner roles, programme scoping, consent-aware access checks and auditable administrative actions.

## Scope

- Partner sponsor, programme manager, analyst and privacy/audit role definitions.
- Programme-scoped authorization.
- Audit events for configuration, access, exports, suspension and closure.
- Explicit-deny behaviour for individual homeowner/property/document/task data.
- Operator impersonation or break-glass behaviour only if justified and fully audited.

## Implementation Workstreams

1. **Scoped access persistence:** add a reusable partner-programme access assignment linking an existing verified HomeTruth user to one partner and programme, with one governed role, active/revoked state, grant/revoke evidence and no homeowner membership semantics.
2. **Server-side policy:** centralise the role/capability matrix and require an active assignment, matching partner/programme scope and applicable programme lifecycle state on every partner endpoint. Admin status must not implicitly grant partner access, and browser-supplied scope must never be authoritative.
3. **Operator assignment controls:** let HomeTruth administrators list, grant, change and revoke partner staff access for a programme without exposing a general user directory or granting partner self-service configuration.
4. **Partner access surface:** provide a partner-facing programme workspace that shows only assigned programme summaries, the current role, allowed capabilities and the aggregate-only privacy boundary. Do not expose evidence metrics before HT-331.
5. **Audit and explicit denial:** record access grants, role changes, revocations, programme/audit views and denied attempts. Partner routes for homeowner, property, document and task resources must fail closed and return no identifying data.
6. **Compatibility:** preserve HomeTruth administrator operations and homeowner product access while making the policy reusable by HT-331 reporting and later shared-core integrations for all supported partner types.

## Out Of Scope

- General enterprise identity architecture.
- SSO or SCIM before an accepted partner requirement.
- Individual report sharing; that remains a separate explicit-consent product path.

## Acceptance Criteria

- [x] Each partner-facing role has documented allowed and denied actions.
- [x] Authorization is enforced server-side by partner and programme scope.
- [x] Individual homeowner, property, document and task resources are denied by default.
- [x] Administrative changes produce reviewable audit records, and the audit schema reserves governed report-view and report-export event types for HT-331.
- [x] Programme status changes immediately affect applicable access; consent and threshold checks remain mandatory before HT-331 exposes any report access.
- [x] Negative authorization and audit tests pass.
- [x] A feature branch, one draft PR per implementation repository and a clean base-branch review loop are completed.

## Dependencies

- HT-328 scope gate accepted.
- HT-329 programme lifecycle administration.
- HT-330 programme-aware acquisition and consent contract.

## Review Gate

Decision recorded 2026-08-03:

- HT-332 precedes HT-331 because the partner evidence dashboard must reuse an established programme-scoped authorization and audit contract.
- A partner access assignment is separate from cohort membership and never makes a partner staff user a PropertyPerson or gives access to homeowner records.
- The shared roles are `sponsor`, `programme_manager`, `analyst` and `privacy_auditor`; all are programme-scoped and fail closed outside that scope.
- HomeTruth administrators remain the only users who grant, change or revoke partner access in this workstream. Partner self-service programme configuration, SSO and SCIM remain out of scope.
- HT-332 implements governed programme-summary and audit capabilities. Aggregate report view/export capabilities are defined for reuse but are exposed only by HT-331 after thresholding, metric-definition and consent-aware reporting gates pass.
- Paused and closed programmes cannot expose partner operational or reporting capabilities. Historical audit review may remain available to an authorised privacy auditor so lifecycle changes and denials remain reviewable.
- No partner role grants individual homeowner, property, document, task, chat, profile or behavioural-event access. A separate future product path would require an approved purpose and explicit individual consent.
- No break-glass or operator impersonation path is justified for this workstream; none will be added.

## Required Verification

- Record migration status before and after the HT-332 schema change; apply, rollback and re-apply it against local MySQL.
- Run syntax checks for every changed backend JavaScript file and `git diff --check` in each implementation repository.
- Add a focused policy verifier covering all four roles and all four partner types, matching and non-matching partner/programme scopes, active/revoked assignments, paused/closed lifecycle behaviour, admin separation, explicit individual-resource denials and privacy-safe response fields.
- Run a real local MySQL smoke with fixture cleanup for assignment grant/change/revoke, duplicate protection, immediate authorization changes and audit evidence.
- Run the existing lifecycle, acquisition and pilot-reporting verifiers to protect HT-329, HT-330 and aggregate reporting compatibility.
- Add focused frontend tests for role/capability presentation, empty/denied/lifecycle states and admin assignment payloads.
- Run the frontend production build, changed-file lint and `git diff --check`.
- Browser-smoke the exact frontend feature head for each partner role, operator grant/change/revoke, cross-programme denial, paused/closed behaviour, explicit privacy boundary, keyboard/focus states and 390px mobile layout.
- Complete the base-branch review/fix loop and record PR URLs, base/head SHAs, final local gates, CI, mergeability and target-environment gaps before closure.

## Implementation Evidence

Implementation date: 2026-08-03. The ticket remains open until both implementation PRs merge.

### Pull Requests

- Backend: https://github.com/jasonlryan/HomeTruth-be/pull/7
  - base: `main` at `4fc46ee1ddbd8843be0540d039c007d82db9dd8f`
  - reviewed head: `6f0aeb3e033480242b32fd1ab2452207c3613819`
  - draft while this evidence was recorded
- Frontend: https://github.com/jasonlryan/HomeTruth-fe/pull/5
  - base: `main` at `52352e7ec5bd6575da1e58f2f794321d335595a2`
  - reviewed head: `43688730b16aa393617e8e6d7fb07f241afcb4d5`
  - draft while this evidence was recorded

### Delivered Boundary

- A reusable assignment and role model covers insurers, mortgage providers, home developers and other B2B clients through one shared policy.
- HomeTruth administrators can grant, change and revoke programme access for an exact verified account email. There is no partner self-service configuration or general user directory.
- Partner access requires an active assignment and exact partner/programme scope. Programme operational access fails closed outside active lifecycle state; authorised historical audit remains available where the role contract permits it.
- Partner responses contain programme and partner summaries, role, current implemented capabilities and the fixed aggregate-only privacy boundary. They contain no homeowner identifiers or individual records.
- Explicit partner routes for homeowner, member, property, document, task, profile, chat and behavioural-event resources deny access and record the attempt without returning identifying data.
- Access and programme lifecycle events are combined into a privacy-safe audit response using only coarse actor categories.
- HT-331 must reuse this authorization service and add consent, minimum-cohort threshold, metric-definition and export gates before any aggregate evidence is returned. HT-332 exposes no report or export endpoint.

### Base-Branch Review/Fix Loop

Both complete `main...feature/ht-332-governed-partner-access` diffs were reviewed from clean, current base worktrees. Findings were fixed and the complete diffs were reviewed again.

- Backend fixes: fail-closed partner/programme consistency in all access discovery paths; non-noisy access-status discovery; programme-summary and lifecycle audit coverage; coarse audit actor categories; removal of future report capabilities from current responses; safe concurrent duplicate handling; corrupt-scope smoke coverage.
- Frontend fixes: durable 403 presentation after stale-summary refresh; role-aware inactive-state copy; access-status sidebar discovery; removal of future report capability assumptions; coarse actor presentation with unknown fail-safe; stale mutation feedback clearing.
- Second review result: no remaining actionable findings.

### Final Local Verification

- Migration recorded down before application, applied, rolled back, re-applied and ended `up` for `20260803150000-create-partner-programme-access.js`.
- Syntax checks passed for every changed backend JavaScript file.
- Partner-access policy verifier and real-MySQL smoke passed across all four roles and all four partner types, including grant/change/revoke, duplicate, revoked, cross-programme, corrupt-scope, lifecycle, explicit individual-resource denial, audit and privacy assertions.
- Existing lifecycle, acquisition and pilot-reporting verifiers passed; existing lifecycle and acquisition MySQL smokes passed.
- Frontend focused tests passed: 3 suites, 12 tests.
- Changed-file ESLint and production build passed. Build output contains only two pre-existing unrelated unused-variable warnings plus existing Browserslist and bundle-size notices.
- Exact-head browser review passed for all four roles and all four B2B partner types; active, paused, closed, empty, denied, audit, admin validation/grant/change/revoke and 390px states had zero console errors.
- `git diff --check` passed in both implementation repositories.

### CI and Remaining Gap

- GitGuardian security checks passed on both reviewed heads while the PRs were draft.
- No review requests or review threads were present when this evidence was recorded.
- Target-environment migration, deployment and smoke have not been run. This is a deployment-stage gap, not a local clear-to-merge claim.
