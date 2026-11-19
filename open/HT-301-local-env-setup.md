# HT-301: Make the local-only environment explicit

Status: In progress — 19 November 2026

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
