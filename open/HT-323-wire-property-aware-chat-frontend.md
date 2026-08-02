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

- [ ] Smoke data includes at least one property-linked document/fact/task.
- [ ] Smoke data includes another property or unrelated user document that should not be retrieved.
- [ ] Property-scoped chat response uses selected-property context.
- [ ] Property-scoped chat response excludes unrelated property/user context.
- [ ] No-property chat mode still follows the documented all-current-user-document fallback.
- [x] Local backend boundary script verifies user/document Qdrant scoping and empty property document scope does not fall back to all user vectors.

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
