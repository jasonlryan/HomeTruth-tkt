# HT-325: Add knowledge-base docs loader

**Priority:** P2
**Repo:** backend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-08-02
**Updated:** 2026-08-02

## Goal

Provide a repeatable backend script for loading the HomeTruth documentation corpus into the Qdrant HomeTruth knowledge-base collection.

## Objective

Add an operator-run command that indexes markdown/text files from the HomeTruth docs repo into MySQL `documents` metadata and Qdrant `home_truth_documents` vectors using real OpenAI embeddings.

## Scope

### In Scope

- Add a backend script for walking a docs directory and indexing `.md` and `.txt` files.
- Use existing `documents` metadata storage for imported knowledge entries.
- Use existing Qdrant `home_truth_documents` collection and vector payload shape.
- Remove a previously imported docs entry before re-importing the same source path.
- Add an npm script entry point for operators.
- Update the Qdrant JS client dependency if needed by the local loader/runtime.

### Out Of Scope

- Automatic scheduled syncing of docs.
- Production deployment or one-time production import execution.
- Admin UI changes for knowledge-base import.
- Changes to property-aware retrieval behavior.

## Acceptance Criteria

- [x] Backend exposes an npm script for loading docs into the knowledge base.
- [x] Loader defaults to the local HomeTruth docs folder and accepts an override path.
- [x] Loader indexes markdown/text files into MySQL `documents` rows and Qdrant points.
- [x] Loader is re-runnable without duplicating prior imports for the same source path.
- [x] Loader requires a real OpenAI API key before embedding work starts.
- [x] Script passes syntax validation.
- [x] Any full import smoke is recorded, or explicitly deferred with the external dependency called out.

## Implementation Log

### 2026-08-02
- Repo: backend, tickets
- Changed:
  - `package.json`
  - `package-lock.json`
  - `scripts/loadKnowledgeBaseFromDocs.js`
  - `HomeTruth-tickets/open/HT-325-knowledge-base-docs-loader.md`
- Verification:
  - Inspected existing `TextSplitter`, `VectorStore`, `OpenAIEmbeddingService` and `documents` model compatibility.
  - `node --check scripts/loadKnowledgeBaseFromDocs.js` passes.
  - Invalid `KB_EMBED_BATCH_SIZE=0` fails fast before DB/Qdrant import work starts.
- Notes:
  - Full import smoke intentionally remains pending until the operator confirms the target docs corpus and whether to write local MySQL/Qdrant knowledge-base state.
