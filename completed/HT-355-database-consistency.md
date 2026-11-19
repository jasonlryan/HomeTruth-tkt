# HT-355 Database consistency and bounded chat history

Status: Completed — merged 19 November 2026

## Objective
Align Sequelize and migrations on plural chat/waitlist tables without data loss. Restore missing indexes and foreign keys and bound chat history retrieval.

## Scope
Explicit table names, forward migration with collision/orphan checks, plural indexes, quiz answer and saved note foreign keys, validated chat pagination and regression tests. Preserve existing record identifiers and responses where compatible with pagination.

## Out of scope
Production deployment, ontology expansion, deleting conflicting records, unrelated worktree changes.

## Acceptance criteria
- Existing plural records retain IDs and values.
- Singular-only installations migrate safely. Conflicting dual-table data stops safely for reconciliation.
- All intended foreign keys and indexes exist on canonical tables.
- History queries enforce finite limits and deterministic ordering with pagination metadata.
- Test fresh and existing schemas, conflicts, retries and API invalid inputs.
- Review feature PR against main and record exact validation evidence before closure.

## Verification — 2026-11-19

- Backend PR https://github.com/jasonlryan/HomeTruth-be/pull/12
  - Base 0e0969035eb4c8afae1f2a014ea3d605038f7fb0
  - Head 2d43b61aec8416c0e2bfbd82a311808e52f96093
- Frontend PR https://github.com/jasonlryan/HomeTruth-fe/pull/14
  - Base aa063c7f366c3db0ba61af127e0721bb166e6633
  - Head 13fe3c67ce63d54a09e2d123b22a5a5bce202832
- Six backend tests and 38 frontend tests passed. Frontend build passed with existing Browserslist/bundle-size warnings. Sidebar tests emitted existing act warnings.
- Read-only controller execution against the MySQL copy verified conversation aggregation and history pagination.
- Local backup saved with mode 0600 to .local-backups/ht355-before.sql before mutation. Restore into dedicated verification database passed.
- Fresh database ran the complete migration sequence successfully. Singular-only populated table migrated successfully. Conflicting dual-table data and orphan references failed safely. Repeated migration succeeded.
- Applied migration to local hometruth. 48 tables became 44. Compared every retained table's full records before/after: identical. Recorded migration in SequelizeMeta and verified both foreign keys.
- Full diffs reviewed from clean main worktrees. Review cleanup committed only on feature branches. No remaining actionable findings. Both feature worktrees clean and pushed.
- Automated GitHub checks currently expose GitGuardian Security Checks, which passed. Test/build validation performed locally.
- Source changes await PR merge/deployment. Production database was not accessed or migrated. Authenticated browser smoke test was not performed; frontend interaction regression tests and production build passed.
- Existing general-chat clients follow all pages for compatibility; the browser still assembles complete conversation summaries. Document history exposes explicit older-page loading.
- Migration is forward-only. Populated singular and plural tables require deliberate reconciliation rather than ID guessing. Recovery uses the verified backup.
- Ticket remains open pending PR handoff/merge evidence. Ticket repository has unrelated existing divergence and edits; no unrelated changes included.


## Final review and merge — 19 November 2026

- Reviewed both PRs and fixed a document-switch race in the frontend. Pending preview, history and answer requests now verify the selected document generation before updating state. Regression coverage proves an older page for Home A cannot populate Home B.
- Frontend main was merged into the feature before validation. Final feature head 6fc87443ceeedd7d0491b74d3d7e5b6bd984bdf4 passed 39 tests and the production build. Backend head 2d43b61aec8416c0e2bfbd82a311808e52f96093 passed all six tests.
- Full diffs and surrounding callers reviewed. No remaining actionable findings or unresolved GitHub review threads. GitGuardian checks passed on the final heads; GitHub exposed no separate test/build CI jobs. Local test/build gates supplied that evidence.
- Backend PR #12 merged to main as 850316e5a2c406cf264f38e262f992a6af54b761.
- Frontend PR #14 merged to main as 40e1068dfd56c144e89e88ecf897aa8ede59b6e5.
- All code fixes were made on feature branches. Production rollout/migration and authenticated browser smoke testing remain outside the verified completion evidence. The local database migration and retained-data comparison passed earlier as recorded above.


## Local browser smoke test — 19 November 2026

- Tested the merged backend main at 850316e5a2c406cf264f38e262f992a6af54b761 and frontend main at 40e1068dfd56c144e89e88ecf897aa8ede59b6e5 against the real local MySQL database and API. This supersedes the earlier browser-testing gap; production remains unverified.
- Authenticated dashboard, existing Ask HomeTruth conversations, Vault document previews and saved document questions loaded successfully.
- Exercised document pagination using a browser request override reducing the real API page limit to two. Loading page two returned HTTP 200 and increased visible questions from two to four. Responses were not mocked; the override was then removed.
- Switching from the survey to the invoice showed only the invoice history. Submitted one labelled local smoke-test question on repair-invoice.pdf; the answer correctly reported GBP 360.00 and unknown payment status. Closing and reopening the document retrieved the saved answer. This test question and answer remain in the fictional Maya Demo account.
- Initial testing used the temporary frontend on 127.0.0.1:3018. Found an older HT-348 preview shadowing port 3000; stopped that preview and verified the normal app at http://localhost:3000/documents?preview=23, including the saved answer. Restarted the backend with the merged code. No application code fix was needed.
- Browser console reported zero errors and zero warnings. Removed the temporary port-3018 preview and temporary authentication-state files; the normal local frontend and backend remain running.
