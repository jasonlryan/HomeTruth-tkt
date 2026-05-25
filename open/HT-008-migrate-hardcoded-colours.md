# HT-008: Migrate hardcoded frontend colours to canonical tokens

**Priority:** P2
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Goal

Replace hardcoded brand colour values and legacy colour utility names in the
frontend with the canonical HomeTruth `ht.*` Tailwind namespace introduced by
HT-306.

## Description

The frontend now exposes canonical HomeTruth design tokens through Tailwind and
CSS custom properties. The app still contains many hardcoded colours and legacy
aliases such as `primary`, `myblue`, `customActiveText`, `customActiveBlue` and
old cyan/orange/purple hex values.

Migrate brand-colour usages to `ht.*` classes where the intent is clear. Keep
neutral/layout colours only when they are genuinely non-brand UI chrome. Any
unclear colour decision should be logged in the implementation notes rather than
silently guessed.

Depends on HT-306.

## Files

- `src/components/**/*.jsx` — brand colour usages
- `src/pages/**/*.jsx` — brand colour usages
- `src/index.css` — remaining hardcoded brand colour values
- `tailwind.config.js` — remove legacy aliases once no usages remain

## Acceptance Criteria

- [ ] Brand colour JSX usages are migrated to `ht.*` Tailwind classes.
- [ ] Legacy colour utility names are removed from JSX where practical:
  `primary`, `myblue`, `customActive`, `customActiveText`, `customActiveBlue`,
  `customBlue`, `softBlue`, `blurpleLight`.
- [ ] Any remaining hardcoded brand colour values are listed in the
  implementation log with a reason.
- [ ] `tailwind.config.js` retains only compatibility aliases that still have
  active usage, with deprecated aliases clearly marked.
- [ ] `npm run build` passes, or the ticket records why verification could not
  be run.
- [ ] A visual review is performed on the highest-risk changed screens:
  nav/header, auth pages, dashboard, document/chat surfaces and article pages.

## Notes

This is intentionally separate from HT-306. HT-306 created the token bridge;
this ticket performs the migration. Older tickets that mention standardising to
`#00c0f9`, `#19B0F0`, `#00bfff`, `#fd6916` or `#c084fc` should be reconciled
against the canonical design-system tokens before implementation.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: migrated the first visible slice — navbar, Home Truths listing,
  article detail and resources page brand-colour usages — from hardcoded cyan /
  purple values and `myblue` aliases to canonical `ht.*` Tailwind classes.
- Verification: `npm run build` completed successfully. The build still reports
  existing unused-variable warnings in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`; those warnings pre-date this slice.
- Notes: `Resources.jsx` still contains hardcoded neutral/tint layout colours
  such as `#f8fafc`, `#f0f7ff`, `#1e2e5c` and `#111827`. These were left in
  place because this slice only migrated clear brand-colour intent. Remaining
  high-risk surfaces for HT-008 are auth pages, dashboard, document/chat
  surfaces, settings and quiz flows.

### 2026-05-25

- Repo: frontend
- Changed: migrated auth and pre-launch surfaces — login, register, admin
  login, forgot password, welcome and coming-soon pages — from legacy
  `customActiveText`, `primary`, old focus-ring blues and hardcoded CTA colours
  to canonical `ht.*` Tailwind classes.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: this preserves the current cyan CTA visual direction while moving the
  implementation to tokens. The design-system still needs component-level
  button guidance to decide when product CTAs should use cyan vs the canonical
  orange `action-primary` token.

### 2026-05-25

- Repo: frontend
- Changed: migrated marketing/static surfaces — about, pricing, pro features,
  FAQ, privacy policy, terms of service, final CTA, call-to-action,
  who-we-help, premium features, pricing plans and trust/security components —
  from hardcoded brand hex values, legacy colour aliases and arbitrary brand
  gradients to canonical `ht.*` Tailwind classes.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted marketing/static files now have no remaining matches for the
  migrated hardcoded brand-colour patterns. Remaining HT-008 work is dashboard,
  admin, document/chat, settings, budget and quiz surfaces, followed by visual
  review of the highest-risk screens.

### 2026-05-25

- Repo: frontend
- Changed: migrated the logged-in app shell and dashboard surface — authenticated
  layout, sidebar, topbar and dashboard — from legacy active-state aliases,
  hardcoded app background, blue focus rings, action buttons, loading indicators
  and markdown links to canonical `ht.*` classes or neutral Tailwind colours.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted app-shell/dashboard files now have no remaining matches for
  the migrated hardcoded brand-colour patterns. Semantic red/green document
  status colours were left unchanged. Remaining HT-008 work is admin,
  document/chat, settings, budget and quiz surfaces, followed by visual review.

### 2026-05-25

- Repo: frontend
- Changed: migrated document and saved-note surfaces — documents list,
  document filters/sorting, upload/reminder states, document Ask HomeTruth modal,
  document preview modal and saved notes — from legacy colour aliases, hardcoded
  blues and arbitrary gradients to canonical `ht.*` classes or neutral Tailwind
  colours.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted document/saved-note files now have no remaining matches for
  the migrated hardcoded brand-colour patterns. Semantic red/green status
  colours were left unchanged. Remaining HT-008 work is chat/assistant, admin,
  settings, budget and quiz surfaces, followed by visual review.
