# HT-307: Define canonical HomeTruth domain model

**Priority:** P1
**Repo:** both
**Created:** 2026-05-25
**Updated:** 2026-05-25

## Goal

Define the canonical HomeTruth domain model before adding more reactive backend tables, so product, frontend, backend, and data work all share the same language for the property record, document vault, evidence, insights, and future enterprise data layer.

Core concept: `Property Register + People Experience = HomeTruth`.

## Description

The current backend database is operational, but it mostly models users, chats, documents, settings, and bookmarked listing blobs. It does not yet model HomeTruth's stated core proposition: the definitive digital record / service log for a home.

This ticket creates a source-controlled domain model artifact from the local HomeTruth product docs, strategy docs, current backend implementation, live database shape, and the NotebookLM domain-model extract supplied in-session. It should separate the immediate canonical model from future or experimental concepts such as blockchain anchoring, psychographic marketplace matching, enterprise report pulls, and contractor credentials.

## Files

- `hometruth DOCS/docs/product/hometruth-domain-model.md` - canonical domain model draft
- `HomeTruth-tickets/open/HT-307-canonical-domain-model.md` - tracking and implementation log

## Acceptance Criteria

- [x] Domain model names the canonical entities and relationships for the HomeTruth property record.
- [x] Domain model separates core MVP/backbone concepts from future or experimental concepts.
- [x] Domain model records invariants that should constrain future backend schema and API design.
- [x] Domain model explicitly compares the target model against the current backend/database gap.
- [x] Follow-up backend implementation tickets can be derived from the model without guessing.
- [x] Ticket implementation log records source material used and verification performed.
- [x] Domain model is reviewed and accepted before backend schema work begins.

## Notes

Do not implement new database tables from the NotebookLM extract directly. First agree the domain language and boundaries, then create focused backend migration/API tickets.

## Implementation Log

### 2026-05-25
- Repo: tickets / product docs
- Changed: created HT-307 and drafted the canonical HomeTruth domain model artifact.
- Verification: source inventory reviewed from local product docs, strategy docs, personas, current backend models/controllers, live local MySQL table list, and NotebookLM extract pasted into the session.
- Notes: ticket remains open pending review/acceptance of the model before backend schema work begins.

### 2026-05-25
- Repo: product docs
- Changed: corrected the modelling principle from property-centred to `property + people`, with `PropertyPerson` as the canonical relationship concept. The first backend implementation may still use `user_properties` if scoped to authenticated users, but the domain language now supports owners, buyers, landlords, tenants, agents, contractors, lenders, insurers, and other people connected to a home.
- Verification: reviewed `hometruth-domain-model.md` after the correction.
- Notes: this keeps HomeTruth from becoming either a property-only ledger or a user-only assistant; the durable product model is the relationship between homes and people.

### 2026-05-25
- Repo: product docs
- Changed: added a business-derived model section to `hometruth-domain-model.md`, grounding `property + people` in `CLAUDE.md`, the product spec, refined proposition, project knowledge, and persona files.
- Verification: searched local product, strategy, and persona docs for homeowners, homebuyers, landlords, investors, contractors, service providers, insurers, lenders, property management, relationship, and psychographic context.
- Notes: the domain model should be treated as business-derived: people make property decisions; properties accumulate facts; HomeTruth is the trusted layer between them.

### 2026-05-25
- Repo: product docs
- Changed: promoted the pitch thesis into the domain model core concept: `Property Register + People Experience = HomeTruth`. Added Width/Depth language from pitch materials: the property register provides national address coverage; the people experience creates depth through consented user participation, evidence, documents, maintenance, decisions, and partner use.
- Verification: reviewed pitch sources including `hometruth DOCS/index.html`, `investor-decks/hometruth-width-depth.html`, `monty-hub/02-thesis.html`, `monty-hub/06-press-kit.html`, and `hometruth DOCS/hometruth-story.html`.
- Notes: future schema work should preserve this concept. Property register without people is static data; people experience without the register is just an assistant. HomeTruth is the compound system.

### 2026-05-25
- Repo: product docs
- Changed: added a graph-ready architecture constraint to `hometruth-domain-model.md`: MySQL remains the source of truth now, but relationship tables, property facts, evidence sources, confidence, provenance, and time windows must be shaped so the data can later be projected into a knowledge graph.
- Verification: reviewed the relationship model and graph projection examples in the domain model.
- Notes: decision is graph-ready, not graph-first. Do not introduce a graph database until relational schema, facts, evidence, and query needs are proven.

### 2026-05-25
- Repo: tickets / backend docs
- Changed: derived HT-308 from the accepted direction of HT-307 and created the backend schema contract for the first property + people database spine.
- Verification: checked current backend document/user/listing model shape before writing the schema spec.
- Notes: HT-307 remains open pending explicit review/acceptance of the canonical model. HT-308 remains a schema-spec ticket only; migration implementation should wait for HT-309.

### 2026-05-25
- Repo: tickets
- Changed: marked the canonical domain model as reviewed and accepted for the first implementation spine.
- Verification: user approved proceeding from the property + people model into HT-308 and HT-309 implementation work.
- Notes: acceptance applies to the working spine, not to a final exhaustive HomeTruth schema.
