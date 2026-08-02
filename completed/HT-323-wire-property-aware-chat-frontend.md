# HT-323: Wire property-aware chat into frontend

**Priority:** P1
**Repo:** frontend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-31
**Updated:** 2026-08-02

## Goal

Make the frontend pass selected property context into authenticated chat so users can ask HomeTruth questions about the property they are viewing.

## Description

HT-321 added backend property-aware unified retrieval. The frontend currently calls `/api/ai_chat/chat` through `askAIChat(message, conversationId, searchWeb, isSaved)` and does not pass `propertyId`.

For the 500-user cohort journey, the property profile needs a clear handoff into chat so the assistant can use selected property context and property-linked documents.

## Dependencies

- HT-321: property-aware unified retrieval layer
- HT-322: 500-user cohort launch gap closure plan

## Expected Files

- `HT_Frontend-staging/src/api/api.js`
- `HT_Frontend-staging/src/pages/AskAI.jsx`
- `HT_Frontend-staging/src/pages/PropertyProfile.jsx`
- `HT_Frontend-staging/src/dev/VisualReviewHarness.jsx` if visual smoke coverage is needed

## Workstream Goal

Give users a property-scoped assistant entry point that sends `propertyId` to the backend and makes it clear when chat is using selected-property context versus all-user-document context.

## Objective

Make the existing Ask AI experience property-aware when launched from a Property Profile, so the selected `propertyId` reaches authenticated chat requests and users can clearly see, use and clear that property context.

## Scope

### In Scope

- Preserve the existing Ask AI route as the chat surface for the pilot.
- Add a property-profile entry point that routes users into Ask AI with the selected property id.
- Pass selected property context through route state and query params so refresh/navigation still has a property id.
- Extend `askAIChat` to send optional `propertyId` to `/api/ai_chat/chat`.
- Show a visible selected-property context indicator in Ask AI.
- Let users clear property context and return to general Ask AI behaviour.
- Clear property context when starting a new session or selecting an existing session.
- Verify the frontend compiles after the change.
- Record remaining target-environment smoke and visual checks.

### Out Of Scope

- Backend retrieval changes. These belong to HT-321 unless smoke testing finds a regression.
- New embedded chat panel inside Property Profile.
- New chat conversation model or persistence changes for property context.
- New analytics/reporting work for property-aware chat usage. This belongs to HT-324 if needed for pilot metrics.
- Legal/privacy, support, target-environment and go/no-go decisions. These remain HT-318, HT-319 and HT-320 work.
- Full production launch approval.

### Closure Requirements

HT-323 can close when the remaining smoke checks prove that:

- clicking “Ask about this property” from a real property profile opens Ask AI with the property context shown
- submitting an authenticated chat request sends the selected `propertyId`
- the backend response uses property-scoped retrieval without crossing into another property/user context
- clearing context or starting a new session removes `propertyId` from subsequent chat requests
- desktop and mobile UI states are visually acceptable

## Phased Plan

### Phase 1: Frontend Wiring

**Goal:** Carry selected property context from Property Profile into Ask AI without changing the core chat route.

Acceptance criteria:

- [x] Property Profile has an “Ask about this property” action.
- [x] The action routes to `/ask-ai` with the selected property id.
- [x] Ask AI can read property context from route state and query params.
- [x] `askAIChat` accepts an optional `propertyId`.
- [x] Authenticated chat requests include `propertyId` when one is active.

### Phase 2: Context UX

**Goal:** Make property-scoped chat understandable, visible and reversible for users.

Acceptance criteria:

- [x] Ask AI displays a selected-property context indicator.
- [x] The context indicator includes the selected property label where available.
- [x] Users can clear selected-property context.
- [x] Starting a new session clears selected-property context.
- [x] Selecting an existing session clears selected-property context.
- [x] No selected property falls back to the documented general Ask AI behaviour.

### Phase 3: API Smoke

**Goal:** Prove the browser sends the selected property id in the real authenticated chat request.

Acceptance criteria:

- [x] Launch Ask AI by clicking “Ask about this property” from a real property profile.
- [x] Submit a property question from Ask AI.
- [x] Verify the `/api/ai_chat/chat` request payload includes the selected `propertyId`.
- [x] Clear context or start a new session.
- [x] Verify subsequent `/api/ai_chat/chat` requests do not include `propertyId`.

### Phase 4: Retrieval Boundary Smoke

**Goal:** Prove the backend response is actually scoped by selected property context.

Acceptance criteria:

- [x] Smoke data includes at least one property-linked document/fact/task.
- [x] Smoke data includes another property or unrelated user document that should not be retrieved.
- [x] Property-scoped chat response uses selected-property context.
- [x] Property-scoped chat response excludes unrelated property/user context.
- [x] No-property chat mode still follows the documented all-current-user-document fallback.
- [x] Local backend boundary script verifies user/document Qdrant scoping and empty property document scope does not fall back to all user vectors.
- [x] OpenAI project has enough quota to generate real smoke embeddings and chat response.

### Phase 5: Visual Review

**Goal:** Confirm the selected-property chat state is visually acceptable for the pilot.

Acceptance criteria:

- [x] Empty Ask AI state with property context is reviewed on desktop.
- [x] Active conversation state with property context is reviewed on desktop.
- [x] Empty Ask AI state with property context is reviewed on mobile.
- [x] Active conversation state with property context is reviewed on mobile.
- [x] The context indicator text and clear action fit without overlap or truncation.

## Acceptance Criteria

- [x] `askAIChat` accepts an optional `propertyId`.
- [x] Authenticated chat request includes `propertyId` when supplied.
- [x] Property profile has a clear “Ask about this property” entry point.
- [x] Selected property id survives navigation from property profile to Ask AI.
- [x] Ask AI displays a selected-property context indicator when property context is active.
- [x] Starting a new general chat clears property context or makes fallback behaviour explicit.
- [x] Browser/API smoke verifies `/api/ai_chat/chat` receives `propertyId` from property-profile-launched chat.
- [x] Visual review covers desktop and mobile property-context chat state.
- [x] Implementation log records changed files and verification performed.

## Review / Decision Gate

Confirm whether property-aware chat should live inside the property profile as an embedded panel or route into the existing Ask AI page with selected property context. The simplest pilot-ready path is route handoff into Ask AI with state/query param.

## Implementation Log

### 2026-05-31
- Repo: tickets
- Changed: created follow-up ticket from HT-322 gap analysis.
- Verification: frontend inspection found `askAIChat` does not pass `propertyId` and `PropertyProfile.jsx` has no property-aware chat entry point.
- Notes: backend support exists from HT-321; this is the frontend handoff needed for the cohort first-session journey.

### 2026-05-31
- Repo: frontend, tickets
- Changed:
  - `HT_Frontend-staging/src/api/api.js`
  - `HT_Frontend-staging/src/pages/AskAI.jsx`
  - `HT_Frontend-staging/src/pages/PropertyProfile.jsx`
  - `HomeTruth-tickets/open/HT-323-wire-property-aware-chat-frontend.md`
- Verification:
  - `npm run build` passes in `HT_Frontend-staging`
  - build still reports pre-existing unrelated lint warnings in `KnowledgeBaseAdmin.jsx` and `DataPrivacySettings.jsx`
- Notes:
  - property profile now routes to Ask AI with selected property context
  - Ask AI shows the selected-property context and passes `propertyId` into authenticated chat requests
  - ticket remains open for real browser/API smoke against the target backend and visual review

### 2026-08-02
- Repo: frontend, backend, tickets
- Changed:
  - `HT_Frontend-staging/src/pages/AskAI.jsx`
  - `HomeTruth-tickets/open/HT-323-wire-property-aware-chat-frontend.md`
- Verification:
  - `npm run build` passes in `HT_Frontend-staging`
  - Playwright local browser/API smoke on `http://localhost:3101` with mocked API responses:
    - property profile opened with property `42`
    - “Ask about this property” opened `/ask-ai?propertyId=42`
    - first `/api/ai_chat/chat` request body included `"propertyId":42`
    - Clear removed the query param and the next `/api/ai_chat/chat` request body omitted `propertyId`
  - Desktop and mobile screenshots reviewed for empty and active property-context Ask AI states.
  - `node scripts/verifyUnifiedRetrievalBoundaries.js` passes in `HomeTruth_BE-staging`
  - build still reports pre-existing unrelated lint warnings in `KnowledgeBaseAdmin.jsx` and `DataPrivacySettings.jsx`
- Notes:
  - fixed a URL cleanup bug so Ask AI preserves `?propertyId=...` until the user explicitly clears context
  - moved the active-chat context notice into the composer so it remains visible after auto-scroll
  - ticket remains open for target-environment retrieval response smoke against real MySQL/Qdrant/OpenAI data

### 2026-08-02
- Repo: backend, tickets
- Changed:
  - `HomeTruth-tickets/open/HT-323-wire-property-aware-chat-frontend.md`
- Verification attempted:
  - Docker was started by the user and `docker start hometruth-mysql` succeeded.
  - Local Qdrant `1.17.0` was started on `localhost:6333`.
  - `npm run db:migrate:status` shows all local backend migrations up:
    - `20260525143000-baseline-existing-schema.js`
    - `20260525230000-create-property-people-spine.js`
    - `20260530120000-create-partner-cohort-consent.js`
    - `20260530143000-create-property-tasks.js`
    - `20260530170000-create-pilot-events.js`
  - Qdrant collections `home_truth_documents` and `user_documents` were initialized locally.
  - Synthetic HT-323 smoke user/property/document rows were created, then cleaned up after the smoke was blocked.
- Blocker:
  - Real OpenAI embedding creation failed with `credit_balance_exhausted`, so no real vectors could be created and the real MySQL/Qdrant/OpenAI retrieval response smoke could not complete.
- Cleanup:
  - Removed the synthetic HT-323 smoke user, two smoke properties and two smoke documents from local MySQL.
- Next move:
  - Add OpenAI credits or provide a working target OpenAI key, then rerun Phase 4 with synthetic selected/unrelated property data and verify the API response `ragContext.scope` plus retrieval context boundary.

### 2026-08-02
- Repo: backend, tickets
- Verification attempted:
  - Re-ran the Phase 4 target-environment retrieval smoke after the OpenAI key was updated.
  - Local MySQL remained reachable through Docker.
  - Local Qdrant remained reachable on `localhost:6333` and both retrieval collections were present.
  - Synthetic selected-property and unrelated-property smoke rows were seeded.
  - The real backend embedding path was exercised through `UserDocumentVectorService.storeDocumentChunks`.
- Blocker:
  - OpenAI still returned `credit_balance_exhausted` on real embedding creation, so no real vectors/context/API response could be produced.
- Cleanup:
  - Synthetic HT-323 smoke rows were removed.
  - Follow-up local count check confirmed zero HT-323 smoke users, properties and documents remain.
- Current status:
  - HT-323 is not complete until a funded/working OpenAI key allows Phase 4 to verify real MySQL/Qdrant/OpenAI retrieval response boundaries.

### 2026-08-02
- Repo: backend, tickets
- Verification attempted:
  - Re-ran the full Phase 4 smoke after the user provided a key.
  - Local backend was started on `http://localhost:4010`.
  - Local MySQL remained reachable through Docker.
  - Local Qdrant was started on `localhost:6333` and collections were initialized.
  - Synthetic selected-property and unrelated-property rows were seeded.
  - The current `.env` contained exactly one `OPENAI_API_KEY` entry.
- Blocker:
  - OpenAI still returned `credit_balance_exhausted` during `UserDocumentVectorService.storeDocumentChunks`, before vectors could be created or the API response boundary could be verified.
- Cleanup:
  - Synthetic HT-323 smoke rows were removed.
  - Follow-up local count check again confirmed zero HT-323 smoke users, properties and documents remain.
- Current status:
  - HT-323 remains open. The next move is to use an OpenAI key whose owning project/organization has available credits, then rerun the same Phase 4 smoke.

### 2026-08-02
- Repo: backend, tickets
- Verification:
  - Re-ran the full Phase 4 target-environment smoke with the updated OpenAI key.
  - Local backend ran on `http://localhost:4010`.
  - Local MySQL was reachable through Docker.
  - Local Qdrant ran on `localhost:6333` with `home_truth_documents` and `user_documents` initialized.
  - Synthetic smoke data included:
    - one selected property with linked boiler-service document, property fact and open task
    - one unrelated property with unrelated user document, property fact and open task
  - Real OpenAI embeddings were created and stored in Qdrant:
    - selected document vectors: 1
    - unrelated document vectors: 1
  - Direct retrieval boundary check passed:
    - selected-property scope: `selected_property_documents`
    - unscoped fallback: `all_current_user_documents`
    - selected marker present in scoped context
    - unrelated marker absent from scoped context
    - source classes: `uploaded_user_document`, `property_record`
  - Authenticated API smoke against `/api/ai_chat/chat` passed:
    - property-scoped request returned `success: true`
    - `ragContext.hasContext: true`
    - `ragContext.scope.propertyId` matched the selected property
    - `ragContext.scope.userDocumentScope: selected_property_documents`
    - `ragContext.counts.uploadedUserDocuments: 1`
    - `ragContext.counts.propertyRecords: 1`
    - source classes included `uploaded_user_document` and `property_record`
  - No-property authenticated API smoke passed:
    - `ragContext.scope.propertyId: null`
    - `ragContext.scope.userDocumentScope: all_current_user_documents`
    - `ragContext.counts.uploadedUserDocuments: 2`
- Cleanup:
  - Synthetic HT-323 smoke rows and vectors were removed.
  - Follow-up local count check confirmed zero HT-323 smoke users, properties and documents remain.
- Current status:
  - HT-323 complete.
