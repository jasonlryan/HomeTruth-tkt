# HT-359 · HomeTruth ontology in Admin Resources

Make the supplied 19 November 2026 ontology, database atlas and guided walkthrough available in the HomeTruth brand under Admin Resources. Preserve concept selection, relationships, diagram controls and presenter navigation. Show the snapshot date and open on the ontology. Changes to the data model, demo records and external-agent rollout are outside scope.

Verify the Admin entry, role guard, diagram selection, all three views, walkthrough jump and return, small viewport, frontend tests and production build.

Frontend PR https://github.com/jasonlryan/HomeTruth-fe/pull/21 is ready for review. Base 37ca6f6, head 9d68bb7. Production build, 45 tests and GitGuardian passed. Browser checks covered guest redirect, homeowner denial, admin access, selection, presenter jump/return and mobile width. Compared all three embedded documents to the supplied source. No unresolved review threads. Awaiting merge.

PR #21 review loop: returned to draft; repaired graph keyboard focus after activation and stale picker filters in both diagrams. The interactive SVGs expose grouped controls. Rereviewed final head e9364ed against main 37ca6f6. All 45 tests, the production build, isolated Chrome interaction/role/mobile checks and all 15 guide target references passed. No outstanding local findings.
