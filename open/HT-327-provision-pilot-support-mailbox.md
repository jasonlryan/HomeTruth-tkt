# HT-327: Provision and validate the pilot support mailbox

**Priority:** P1
**Repo:** n/a
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-08-02
**Updated:** 2026-08-02

## Goal

Make `support@hometruth.io` a real, tested user-facing support route before it appears in any pilot communication.

## Objective

Provision the mailbox or shared inbox, route it to a monitored recipient or group, verify inbound and outbound delivery, and record the temporary first-response coverage.

## Scope

### In Scope

- Create or confirm the `support@hometruth.io` mailbox/shared inbox.
- Permit inbound mail and replies from the HomeTruth domain.
- Forward or grant access to at least one monitored recipient or shared on-call group.
- Configure a privacy-safe acknowledgement only if it does not promise an unapproved response time.
- Send and receive a test message from outside the mailbox.
- Record temporary coverage: one business-day first response, Monday to Friday, 09:00-17:00 UK time.
- Add evidence to HT-318 once validation passes.

### Out Of Scope

- Permanent support, incident or privacy owner assignment.
- Legal/privacy approval of the deletion runbook.
- Building a support desk, ticketing system or automated triage product.
- Publishing the address before validation is complete.

## Acceptance Criteria

- [ ] `support@hometruth.io` receives a message from an external sender.
- [ ] A monitored person or shared group can view and reply to that message.
- [ ] The reply is sent from the HomeTruth domain.
- [ ] The temporary coverage and first-response target are recorded in HT-318.
- [ ] Any acknowledgement copy has been checked for privacy, security and response-time claims.
- [ ] A test result, date and responsible temporary recipient are recorded in HT-318.
- [ ] HT-318 and HT-322 are updated to reflect the validated route.

## Review / Decision Gate

HT-327 clears the mailbox-validation portion of HT-318. It does not close HT-318 or permit launch until a support owner, technical escalation contact and incident owner are named.

