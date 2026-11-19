# HT-337: Build owner-authorised agent access and revocation

**Priority:** P1
**Repo:** backend / frontend / docs
**Created:** 2026-10-25
**Status:** Planned, not implemented

## Objective

Implement delegated agent authentication and property-scoped grants, distinct from partner staff and OPDA organisation credentials.

## Scope

OAuth discovery/PKCE; verified token claims; property/platform/scopes/purpose; expiry/revocation; safe logs and consent UX.

## Out Of Scope

Partner access to individual data by default, shared admin keys, automatic certification and write permissions.

## Implementation Workstreams

1. Agree and record the bounded contract and unresolved external decisions.
2. Implement on a ticket-named feature branch only after its contract is accepted.
3. Complete focused and dependency-path validation, base-branch review/fixes and one PR per implementation repository.

## Acceptance Criteria

- [ ] Approved contract names the identity provider, grant model and target clients.
- [ ] Server enforces current property and document permissions on every call.
- [ ] Revoked/expired grants and cross-user/property access fail closed.
- [ ] Consent explains selected sharing and that revocation blocks subsequent HomeTruth reads but cannot withdraw information already exported to a recipient.
- [ ] With a valid token and an active, unexpired grant, removing the granting user's property relationship or document permission denies subsequent tool reads and evidence retrieval. Cached authorisation must not bypass current permission checks.
- [ ] Revoking the grant denies subsequent tool reads and evidence-link requests even while the token remains valid.

## Required Verification

Real dependency-path authentication tests; negative tokens/scopes, revocation, isolation, concurrency, consent UX and full feature PR loop.

## Dependencies And Decisions

HT-335 plan: `hometruth DOCS/docs/product/personal-agent-opda-delivery-plan.md`. Follow the workstream sequence and external approval gates there. No technical owner, budget or delivery date is assumed.

## HT-FLOW-005 database requirements

**Reuse.** Use `users`, `properties` and the active `property_people` relationship to identify who can access the home.

**Missing or required.** Authenticate the external client through the agreed OAuth discovery/PKCE flow and verify token claims. The central missing authorisation record is a revocable grant, which must link the granting person, external client, home, purpose, permitted reads and evidence, expiry and revocation. Check the grant and current property and document permissions on every read. Record the grant, operation, time and outcome for access review.

**Decision needed.** Which roles may delegate, which sources may leave HomeTruth, how long can a grant last, and how long should access records be kept?

This records planning requirements only. Connect your agent remains on the roadmap.
