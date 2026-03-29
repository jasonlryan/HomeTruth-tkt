# HT-301: Set up local .env files

**Priority:** P1
**Repo:** both
**Created:** 2026-03-29
**Updated:** 2026-03-29

## Description

Create working .env for backend (local MySQL credentials, own OpenAI API key, skip SendGrid/Zoopla) and update frontend .env to point at localhost backend instead of staging IP.

## Files

- `HomeTruth_BE-staging/.env` — create from .env.template
- `HT_Frontend-staging/.env` — update REACT_APP_API_BASE_URL

## Acceptance Criteria

- [ ] Backend starts and connects to local MySQL
- [ ] Frontend starts and connects to localhost backend
- [ ] No references to team's staging IPs

## Notes

.env.template already created in Cowork folder. Backend auto-creates schema via sync({alter:true}). Seeders populate quiz data and admin user.
