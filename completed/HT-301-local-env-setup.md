# HT-301: Make the local-only environment explicit

Status: Completed — merged and smoke-tested 19 November 2026

## Objective
Remove obsolete previous-team deployment references and configure the current local setup. The owner confirmed that no staging or production environment exists.

## Scope
Local frontend/API settings, obsolete staging commands and environment selection, old CORS origins and UI URLs, tracked setup examples, and environment documentation. Preserve credentials and existing data.

## Out of scope
Provisioning hosting, deployment, database migrations or resets, third-party API integrations, unrelated changes.

## Workstreams
- Backend: local environment loading and CORS; remove misleading staging commands and CLI aliases.
- Frontend: localhost configuration, local property placeholder and extension login; remove staging commands.
- Documentation: local topology, environment precedence and future deployment prerequisites.

## Acceptance criteria
- No obsolete previous-team deployment hosts in active source/configuration.
- Local frontend uses localhost:3000 and API localhost:8005; MySQL remains 127.0.0.1:3306/hometruth.
- Selecting unsupported staging/production database configuration cannot silently use the local database.
- No database records, credentials or migrations are changed.
- Both code changes pass relevant checks and feature-branch PR review; docs state that hosted environments do not exist.

## Verification
Source/configuration scan, environment-selection checks, frontend tests/build, full PR diff review and remote check inspection. Historical ticket records are labelled as historical rather than treated as live infrastructure.


## Implementation and verification — 19 November 2026

- Backend PR https://github.com/jasonlryan/HomeTruth-be/pull/15
  - Base: 850316e5a2c406cf264f38e262f992a6af54b761
  - Head: 356d28c6beb2455d87153995b385edb46d75a3b6
- Frontend PR https://github.com/jasonlryan/HomeTruth-fe/pull/17
  - Base: 40e1068dfd56c144e89e88ecf897aa8ede59b6e5
  - Head: 8926f6da22b3e64b73bef4afeaa4556e91f49768
- Code fixes made only on feature/ht-301-local-environment in isolated worktrees. Existing dirty worktrees were preserved. Reviewed full diffs and surrounding callers from clean main review worktrees; no remaining actionable findings. Both heads contain current main, are clean/pushed and mergeable, with no review threads. Marked ready once after local validation. GitGuardian passed; no separate test/build CI jobs were exposed. PRs are not merged.
- Backend syntax/environment checks passed: local/development/test accepted; staging/production rejected before connection; CLI exposes no staging/production aliases. Three pagination regression tests passed.
- All 39 frontend tests passed; final-head build compiled successfully. Existing React act/Browserslist notices remain. Extension script syntax and manifest JSON checked. Full extension authentication was not exercised.
- Tracked-file scan found no obsolete previous-team IPs, playground hosts or preview tunnel hosts in either feature head. Removed the last backend property-image tunnel fallback during review.
- Active ignored frontend .env and .env.development.local now use port 3000 and API localhost:8005; retired .env_staging removed. Verified backend nonsecret endpoints already point locally. Credentials and database data were not changed; no migrations run.
- Published environment-status.md and a delivery-playbook clarification directly to documentation main (06a254e). Historical HT-300 text now explains that previous-team hosts are retired. Local topology is frontend 3000, API 8005, MySQL 3306/hometruth and Qdrant 6333. No hosted staging or production exists.


## Merge and local smoke test — 19 November 2026

- Both PRs passed GitGuardian checks and were merged at the reviewed heads. Backend main: ddeb503a6ccac8bdfbc18f276551ebb62c4952f3; frontend main: 1652fc0b3f1559e2c00b8fa92fa210560028ec81.
- Fast-forwarded the active local checkouts, preserving unrelated .gitignore and public/admin changes. Restarted backend 8005 and frontend 3000 from those checkouts. Frontend compiled successfully.
- Authenticated browser opened the Vault invoice preview and retrieved the previously saved question and GBP 360.00 answer. Local property placeholder returned HTTP 200 and valid SVG content. Browser console: zero errors and warnings.
- Read-only Sequelize status confirmed all 15 migrations applied; none pending. No migrations were run and no records or credentials were changed.
- Full browser-extension login was not part of the quick smoke test. Hosting remains local only.
