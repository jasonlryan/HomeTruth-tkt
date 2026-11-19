# HT-353: Implement scoped parent and child agent messaging

**Repo:** backend
**Priority:** P1
**Created:** 2026-11-19
**Depends on:** HT-351 and HT-352
**Specification:** HomeTruth product docs, `docs/product/agent-sdk-integration.md` (2992cdc).

## Goal

Allow one authorised specialist to request a typed result from another inside the same root run.

## Implementation

Implement server-assigned correlation IDs, typed envelopes, single-level sequential delegation, reply matching and root deadline/token accounting. Deduplicate logical steps. Keep the appliance child allowlist empty.

## Scope boundary

No broker, asynchronous mailbox, external agent connection or production child pair.

## Acceptance criteria

- [ ] An allowed fixture child receives minimal scoped inputs.
- [ ] Reject cycles, unapproved recipients, cross-home references, duplicate keys with changed inputs, over-budget work and late replies.
- [ ] Child failure respects the parent's result schema.

## Verification

Exercise valid request/reply, concurrency, replay, expiry and failure using deterministic fixture agents. Inspect retained metadata after expiry.
