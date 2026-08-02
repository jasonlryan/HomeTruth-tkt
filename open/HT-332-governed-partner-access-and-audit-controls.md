# HT-332: Add governed partner access and audit controls

**Priority:** P1
**Repo:** backend / frontend / docs
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-02

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

## Out Of Scope

- General enterprise identity architecture.
- SSO or SCIM before an accepted partner requirement.
- Individual report sharing; that remains a separate explicit-consent product path.

## Acceptance Criteria

- [ ] Each partner-facing role has documented allowed and denied actions.
- [ ] Authorization is enforced server-side by partner and programme scope.
- [ ] Individual homeowner, property, document and task resources are denied by default.
- [ ] Administrative changes, report access and exports produce reviewable audit records.
- [ ] Consent and programme status changes immediately affect applicable access.
- [ ] Negative authorization and audit tests pass.
- [ ] A feature branch, PR and clean review loop are completed.

## Dependencies

- HT-328 scope gate accepted.
- HT-329 programme lifecycle administration.
