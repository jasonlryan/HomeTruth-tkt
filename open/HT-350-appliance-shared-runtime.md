# HT-350: Route appliance manual lookup through the shared runtime

**Repo:** backend
**Priority:** P1
**Created:** 2026-11-19
**Depends on:** HT-341 appliance backend
**Specification:** HomeTruth product docs, `docs/product/agent-sdk-integration.md` (2992cdc).

## Goal

Give backend callers a versioned invocation contract for the first appliance operation while keeping the existing HTTP and review experience.

## Implementation

Register appliance-information@1/findManual with validated request and result contracts. Bind the authorised service and SDK adapter at startup. Keep the manufacturer policy, limits and import authority in their existing layers. Protect lookup completion against interrupted-run recovery.

## Scope boundary

Durable revision metadata, usage controls and expiry follow in HT-351 and HT-352.

## Acceptance criteria

- [ ] The existing manual-search endpoint calls the dispatcher with server-owned scope and the original request key.
- [ ] Invalid operations and inputs fail before paid work.
- [ ] Review, fallback, reload, duplicate requests and confirmed import retain their existing contracts.
- [ ] Late lookup results cannot revive a recovered run.

## Verification

Run offline appliance and dispatcher regressions including normal route wiring, denial, replay, malformed input and interrupted completion. Review the incremental diff against HT-341.

## Implementation log

19 November 2026. [Backend PR #11](https://github.com/jasonlryan/HomeTruth-be/pull/11) is ready for review against the HT-341 branch at b0805e7. Reviewed and pushed head aa64419. The local route smoke check, 27 offline tests and the isolated MySQL concurrency/persistence suite passed. Concurrent identical invocations made one provider-fixture call. The recovered-run regression rejects a late completion. GitHub reports a clean merge state, zero review threads and a passing GitGuardian check. Application tests ran locally. The ticket remains open pending integration with HT-341.
