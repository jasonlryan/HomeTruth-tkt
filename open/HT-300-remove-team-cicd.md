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

Backend workflow deploys to 3.141.227.135 (staging) and 3.149.116.163 (production). Frontend deploys to 3.141.227.135 and 18.223.231.19. None of these are ours.
