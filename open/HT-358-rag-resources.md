# HT-358 Separate RAG ingestion records and Resources

Show administrators the actual indexed chunks from the shared Qdrant collection. Group HomeTruth articles and platform documentation under Resources. Correct the presentation workspace that currently repeats editorial records under Knowledge.

Scope covers a read-only, admin-authorised Qdrant inventory, navigation, presentation copy and regression checks. Private document collections, reindexing and changes to article publishing are outside scope.

Verify that paginated records come from Qdrant, empty and unavailable states are distinct, and articles and documentation are accessible independently. Exercise both repositories' checks and review each feature PR against main.

## Review evidence
- Frontend [PR 19](https://github.com/jasonlryan/HomeTruth-fe/pull/19), main 5ecf137, head 5e70564. All 45 tests and CI-mode production build passed. Chrome exercised Resources, its documentation link and the RAG inventory on the built feature head with a synthetic admin and API fixtures.
- Backend [PR 18](https://github.com/jasonlryan/HomeTruth-be/pull/18), main 163f2a5, head c2b2a49. All 9 root tests passed. The feature service read two pages of 25 distinct points each from local shared Qdrant with no overlap.
- Clean-main diff reviews complete. Both heads were mergeable with no review threads. Merge the backend first to make the inventory available to the frontend.
