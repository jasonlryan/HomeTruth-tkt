# HT-360 · Resettable investor demo using the product schema

Give the investor demo its own MySQL database, document storage and retrieval index. Use the product's versioned Sequelize migrations and a versioned synthetic fixture pack. Preserve the working database and exclude real accounts, external billing and notifications.

## Delivery sequence
1. Prove the current backend migrations build a clean disposable database. Compare migration history, tables, columns, indexes and foreign keys on repeated builds.
2. Seed curated John and Maya journeys first. Preserve all 13 ledger entries and payment states, Maya's selected-home permissions, two washers, source PDFs, cited answer, survey passage and follow-up. An unfulfilled listed document is not evidence.
3. Import the 1,000 Brighton rows using stable source IDs, property/address/owner relationships and local plan state. Preserve all source fields including original property types. Keep the 1,588 document labels separate from actual files. Mark exports with dataset_id and demo_only.
4. Connect the Admin Data Room, search, Free/Pro filters, CSV/JSON export and ledger drill-down to the demo records. Keep Maya separate from Brighton portfolio totals. Support a demo-only reset and repeatable start with the running product.
5. Verify two resets, 1,000 distinct Brighton homes, 557 Free and 443 Pro, no duplicate associations, no working-data changes and no notifications or billing. Rehearse Admin → John and Maya → Control centre → Vault → Ask on the pinned frontend/backend revisions.

Production deployment and changes to live customer records are outside scope. Any gap requiring new product schema must use a shared migration reviewed by the normal backend workflow.

## Initial verification · 26 November 2026

Ran the unchanged migration chain from backend main 370348fee795cf26ddc0b4fbace074cf3650a651 on a new, empty, disposable MySQL 8 container bound to loopback. All 15 migrations completed and the database contained 45 tables including SequelizeMeta. The container was stopped after verification. No existing database was used or reset. This establishes a clean build; structural parity with the working database, fixture loading, repeatable reset and integrated walkthrough remain open.

## Data verification on 26 November 2026

[Backend draft PR 19](https://github.com/jasonlryan/HomeTruth-be/pull/19) contains the versioned fixture and dedicated local database setup. Two clean resets reproduced the same 45-table schema fingerprint and passed field-by-field reconciliation for all 1,000 Brighton homes, 557 Free and 443 Pro, 1,588 listed documents, 13 John ledger entries and four readable Maya files. A repeat seed on populated data refused to overwrite it.

The working dev database also has 45 tables. A read-only DDL comparison found differences on 19 tables, including timestamp defaults, indexes, column comments and foreign key names. Fresh builds reproduce the migration-defined schema. Reconcile legacy drift through a separately reviewed shared migration before claiming identical structure across environments. The working database was not edited.

Admin portfolio filtering and export, isolated vector retrieval, Maya’s cited journey and the rehearsal on 3014 remain open.

## Investor consolidation, 27 November 2026

[Backend PR 19](https://github.com/jasonlryan/HomeTruth-be/pull/19) merged to main at e814cf4. The loopback product API on 8360 runs from a main checkout with the isolated demo database, private media copies and a local knowledge snapshot. The snapshot reconciled 783 general and 442 URL records from the shared knowledge index into 174 readable documents, without copying private user-document namespaces. Admin browsing and text search work independently of the Styleguide server. No vector-search equivalence is claimed.

Live authenticated checks cover source-faithful Brighton CSV/JSON and ledger CSV, all 1,000 source rows, exact tier totals, Maya exclusion, John's 13 entries and the knowledge list/detail responses. Anonymous and homeowner access checks passed. Nine backend tests and GitGuardian passed. The frontend main browser gate and Maya's provider-assisted missing manual rehearsal are tracked separately pending evidence.

## Frontend consolidation, 27 November 2026

[Frontend PR 22](https://github.com/jasonlryan/HomeTruth-fe/pull/22) merged without squashing from reviewed head 1bad44d into main at 38eea90. Both local frontend checkouts were fast-forwarded to that merge. Main on 3014 passed the authenticated Admin walkthrough with port 3001 blocked.

The walkthrough covered the ontology, four explainers, nine sample cards (two original text previews and seven catalogue-only entries), the byte-identical survey Markdown, and text search and browsing over 174 knowledge documents. Browser downloads reconciled to 1,000 Brighton homes, 557 Free, 443 Pro, 1,588 document labels and 13 John ledger entries. The anchoring demonstration runs in the browser and sends no transaction. Frontend checks: 49 tests, optimized build and GitGuardian passed.

Keep the ticket open for the remaining rehearsal evidence. The Utility washing-machine search has not delivered a verified manual.

On 3014, frontend main 38eea90 and API main 23f9280 passed the Admin walkthrough again after restart. Maya signed in with the local shortcut, selected the Kitchen Bosch WAN28281GB, typed her manual request in Ask HomeTruth, and opened the existing Vault document 4 with zero provider searches. The Utility live-search success case remains open.
