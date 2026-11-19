# HT-300: Remove team CI/CD workflows

**Priority:** P2
**Repo:** both
**Created:** 2026-03-29
**Updated:** 2026-03-29

## Description

Delete .github/workflows/main.yml from both repos. These are configured for the team's AWS EC2 instances and SSH keys — they'll never work on our setup and could cause confusion.

## Files

- `HomeTruth_BE-staging/.github/workflows/main.yml`
- `HT_Frontend-staging/.github/workflows/main.yml`

## Acceptance Criteria

- [ ] No workflow files in either repo or replaced with our own CI/CD if needed

## Notes

Historical ticket: the previous team's AWS staging/production addresses were
not owner-managed environments. The old backend deploy workflow was removed.
As confirmed on 19 November 2026, HomeTruth runs locally only; there is no current
hosted staging or production environment. HT-301 removes remaining obsolete
runtime references and documents local setup. Do not use historical workflows
or old configuration as connection instructions.
