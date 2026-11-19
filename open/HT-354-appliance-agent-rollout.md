# HT-354: Verify and enable the appliance runtime pilot

**Repo:** backend
**Priority:** P1
**Created:** 2026-11-19
**Depends on:** HT-350 through HT-352; HT-353 only for a future delegated workflow
**Specification:** HomeTruth product docs, `docs/product/agent-sdk-integration.md` (2992cdc).

## Goal

Roll out the registered appliance operation with observable outcomes and a reversible routing decision.

## Implementation

Verify parity offline, exercise the homeowner journey from lookup to private import, collect latency, usage, no-match, duplicate and failure counts, and rehearse rollback with outstanding reviews. Obtain owner approval of retention and experience before enablement.

## Scope boundary

No scheduled jobs or external agent pilots.

## Acceptance criteria

- [ ] Exact-model PDF saves once, invalid citations and unsupported brands give fallbacks, and source answers reproduce verified passages.
- [ ] Pending reviews survive rollback.
- [ ] Record exact versions, owner decision and pilot scope.

## Verification

Run database concurrency and import checks, frontend journey checks, and a rollback drill. Record CI and review evidence before pilot enablement.
