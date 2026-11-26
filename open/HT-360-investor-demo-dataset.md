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
