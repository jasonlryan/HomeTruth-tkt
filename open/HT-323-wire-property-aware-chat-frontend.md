# HT-323: Wire property-aware chat into frontend

**Priority:** P1
**Repo:** frontend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-31
**Updated:** 2026-05-31

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

## Acceptance Criteria

- [x] `askAIChat` accepts an optional `propertyId`.
- [x] Authenticated chat request includes `propertyId` when supplied.
- [x] Property profile has a clear “Ask about this property” entry point.
- [x] Selected property id survives navigation from property profile to Ask AI.
- [x] Ask AI displays a selected-property context indicator when property context is active.
- [x] Starting a new general chat clears property context or makes fallback behaviour explicit.
- [ ] Browser/API smoke verifies `/api/ai_chat/chat` receives `propertyId` from property-profile-launched chat.
- [ ] Visual review covers desktop and mobile property-context chat state.
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
