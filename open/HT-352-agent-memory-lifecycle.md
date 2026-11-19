# HT-352: Implement scoped agent memory and expiry

**Repo:** backend
**Priority:** P1
**Created:** 2026-11-19
**Depends on:** HT-351
**Specification:** HomeTruth product docs, `docs/product/agent-sdk-integration.md` (2992cdc).

## Goal

Let a homeowner revisit a lookup while keeping confirmed appliance evidence under its own document lifecycle.

## Implementation

Declare the context projection and memory policy per operation. Extend existing run storage compatibly. Apply the proposed 30-day review window after owner sign-off. Expire transient results and remove derived evidence on deletion.

## Scope boundary

No provider session history or cross-home shared memory.

## Acceptance criteria

- [ ] Expired and legacy reviews follow the agreed policy.
- [ ] Expiry preserves saved manuals.
- [ ] Access loss, source deletion and changed identity prevent stale reads and confirmation. Remove the initiating user’s property access while a review is unexpired, then verify both result retrieval and confirmation fail.
- [ ] Sensitive prompts and documents stay out of logs.

## Verification

Use a controlled clock, migrated legacy records, deletion and cross-owner fixtures. Verify expiry retries and inspect persisted data and logs.

## HT-FLOW-005 database requirements

**Reuse.** Use the run for reviewable candidates, `home_items` for the appliance and `home_item_evidence` for the confirmed document association.

**Missing or required.** Separate temporary review expiry from the confirmed manual’s document lifecycle. Recheck access before reading or importing a candidate. Expiring a review must preserve an already confirmed manual.

**Decision needed.** Approve or revise the proposed 30-day review window and the treatment of legacy runs. External grant expiry is a separate HT-337 decision.

This records planning requirements only. Connect your agent remains on the roadmap.
