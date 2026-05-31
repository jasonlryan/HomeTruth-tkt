# HT-321: Build property-aware unified retrieval layer

**Priority:** P1
**Repo:** backend / docs / tickets
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-31
**Updated:** 2026-05-31

## Goal

Make HomeTruth answer user questions using the right mix of general HomeTruth knowledge, private user documents and property context, without crossing user, property or consent boundaries.

## Description

HomeTruth now has the right storage foundations:

- general/admin knowledge base in `documents` and Qdrant `home_truth_documents`
- private uploaded user documents in `userDocuments` and Qdrant `user_documents`
- property records and property-document links through the property + people spine
- partner/cohort/consent models for the 500-user insurer pilot path

The current retrieval implementation is not yet the finished architecture. The main assistant searches the general knowledge base. Specific document chat searches private user-document chunks. There is not yet one property-aware retrieval layer that safely combines general guidance, private uploaded documents and property record context for a specific authenticated user/property.

This ticket creates that layer before live cohort scale, so the assistant can be useful to many users without leaking private data or mixing the wrong property context.

## Dependencies

- HT-307: canonical HomeTruth domain model
- HT-308: property + people database schema contract
- HT-312: link documents to properties
- HT-314: partner cohort and consent model
- HT-316: homeowner-first prevention and partner access governance
- HT-319: data deletion and consent withdrawal runbook

## Expected Files

- `HomeTruth_BE-staging/services/...` unified retrieval service
- `HomeTruth_BE-staging/services/userDocumentVectorService.js`
- `HomeTruth_BE-staging/services/vectorStore.js`
- `HomeTruth_BE-staging/Controllers/AI/ai_chat.js`
- `HomeTruth_BE-staging/Controllers/userDocumentChatController.js` if shared retrieval applies there
- `HomeTruth_BE-staging/tests/...` or local verification script for retrieval boundaries
- `hometruth DOCS/docs/product/property-aware-retrieval-architecture.md`
- `HomeTruth-tickets/open/HT-321-property-aware-unified-retrieval.md`

## Acceptance Criteria

- [ ] A single backend retrieval service exists for assistant context assembly.
- [ ] Retrieval can search the general knowledge base from Qdrant `home_truth_documents`.
- [ ] Retrieval can search private user documents from Qdrant `user_documents` with a required `user_id` filter.
- [ ] Retrieval supports optional `property_id` scoping for private user documents.
- [ ] User document vectors include enough metadata to support property-aware filtering, either directly in vector payload or through a safe DB join before retrieval.
- [ ] If no `property_id` is supplied, behaviour is explicit: either search all current user's documents or require property selection, with the decision recorded.
- [ ] General KB results and private user document results are labelled separately before being passed to the LLM.
- [ ] Assistant prompts distinguish source classes: uploaded user document, property record/evidence, HomeTruth guidance, and external/web source where applicable.
- [ ] Main authenticated assistant uses the unified retrieval service instead of searching only the general KB.
- [ ] Specific document chat continues to enforce `user_id` and document ownership.
- [ ] Cross-user retrieval is impossible by implementation, not just UI convention.
- [ ] Tests or verification scripts prove User A cannot retrieve User B's vectors.
- [ ] Tests or verification scripts prove property-scoped retrieval does not return another property's documents for the same user.
- [ ] Deletion/withdrawal implications are documented for both MySQL and Qdrant chunks, aligned with HT-319.
- [ ] The implementation remains viable for a 500-user pilot and records the expected vector volume/scaling assumptions.
- [ ] Implementation log records changed files and verification performed.

## Scale Requirements

The design must support the first 500-user cohort without requiring a later rewrite.

Planning assumptions:

- 500 users
- 1-3 properties per active user
- 5-20 uploaded documents per user
- 10-50 chunks per document depending on file length
- expected first-pilot private vector range: roughly 25,000-500,000 vectors

Qdrant can handle this volume. The higher-risk scaling areas are:

- synchronous embedding during upload
- long-running file processing
- idempotent reindexing after metadata changes
- deletion/withdrawal propagation into Qdrant
- retrieval latency when combining multiple source classes

The first implementation can remain simple, but it must avoid architecture that prevents queue-based ingestion, property metadata backfill or hosted Qdrant migration later.

## Retrieval Boundary V1

For an authenticated user question, retrieval should assemble context in this order:

1. Private user document chunks filtered by authenticated `user_id`.
2. If a property is selected, further constrain private chunks to that `property_id` or to documents linked through `property_documents`.
3. Property record/fact/task context visible to the authenticated user.
4. General HomeTruth knowledge from `home_truth_documents`.
5. Optional web search only when explicitly requested and available.

The assistant response should never expose internal scores or raw retrieval metadata, but it should make source class clear in user-facing language where useful:

- "From your uploaded document..."
- "From your property record..."
- "HomeTruth guidance says..."

## Privacy And Consent Rules

- General KB is shared HomeTruth knowledge.
- User documents are private and must be filtered by authenticated user.
- Property-scoped retrieval must not return another property's documents unless the user has intentionally selected all-property context.
- Partner/insurer users receive no individual document, fact, task, property or answer-level data by default.
- Individual partner report access remains out of scope unless a future ticket implements explicit consent and review.
- Aggregate pilot analytics must remain separate from individual retrieval.

## Review / Decision Gate

Review before implementation:

- Should the default assistant require an active property selection, or search all documents owned by the current user when no property is selected?
- Should user document vectors store `property_id` directly, or should property scoping be resolved through `property_documents` before querying Qdrant?
- Should uploaded documents be reindexed when a document is later linked to a property?
- What source labels should be exposed in the UI versus only used inside prompts?
- What minimum deletion/withdrawal behaviour is required before the 500-user pilot?

## Implementation Notes

- Do not merge `documents` and `userDocuments` under this ticket.
- Do not expose partner-facing individual document/report access under this ticket.
- Do not add a graph database under this ticket.
- Keep MySQL as the source of truth; Qdrant is a retrieval index.
- Prefer additive metadata/backfill steps over destructive vector collection recreation.
- If vector metadata is updated, provide an idempotent reindex path.

## Implementation Log

### 2026-05-31
- Repo: tickets
- Changed: created HT-321 for property-aware unified retrieval planning.
- Verification: derived from current backend implementation, loaded Qdrant state, property + people ticket history and 500-user pilot scale requirement.
- Notes: this is the next backend architecture ticket needed before the assistant can safely combine general KB and private user/property documents at cohort scale.
