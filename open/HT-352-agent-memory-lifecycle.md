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
- [ ] Access loss, source deletion and changed identity prevent stale reads and confirmation.
- [ ] Sensitive prompts and documents stay out of logs.

## Verification

Use a controlled clock, migrated legacy records, deletion and cross-owner fixtures. Verify expiry retries and inspect persisted data and logs.
