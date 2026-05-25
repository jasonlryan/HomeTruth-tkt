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

- [x] Brand colour JSX usages are migrated to `ht.*` Tailwind classes.
- [x] Legacy colour utility names are removed from JSX where practical:
  `primary`, `myblue`, `customActive`, `customActiveText`, `customActiveBlue`,
  `customBlue`, `softBlue`, `blurpleLight`.
- [x] Any remaining hardcoded brand colour values are listed in the
  implementation log with a reason.
- [x] `tailwind.config.js` retains only compatibility aliases that still have
  active usage, with deprecated aliases clearly marked.
- [x] `npm run build` passes, or the ticket records why verification could not
  be run.
- [x] A visual review is performed on the highest-risk changed screens:
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

### 2026-05-25

- Repo: frontend
- Changed: migrated guest chat and smaller assistant components —
  `GuestChat.jsx`, `Aiassistant.jsx` and `AskAIA.jsx` — from hardcoded cyan /
  purple values, legacy `myblue` aliases, old focus rings and chat CTA colours
  to canonical `ht.*` classes or CSS-token style values.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted guest-chat/assistant files now have no remaining matches for
  the migrated hardcoded brand-colour patterns. The larger logged-in
  `AskAI.jsx` chat surface remains as its own slice.

### 2026-05-25

- Repo: frontend
- Changed: migrated the logged-in `AskAI.jsx` chat surface — assistant bubbles,
  markdown links, session list active states, save-session prompts, search-web
  toggles, answer input actions, info banners and modal icons — from legacy
  colour aliases, hardcoded cyan/purple/blue values and old indigo panels to
  canonical `ht.*` classes, neutral Tailwind colours or semantic Tailwind
  colours.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: `AskAI.jsx` now has no remaining matches for the migrated hardcoded
  brand-colour patterns. Remaining HT-008 work is admin, settings, budget and
  quiz surfaces, followed by visual review.

### 2026-05-25

- Repo: frontend
- Changed: migrated settings surfaces — account, preferences, notifications and
  data privacy — from legacy `primary`/`customActiveText` aliases, hardcoded
  app backgrounds, blue icon chips, toggles and save/reset buttons to canonical
  `ht.*` classes or neutral Tailwind colours.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted settings files now have no remaining matches for the migrated
  hardcoded brand-colour patterns. Remaining HT-008 work is admin, budget and
  quiz surfaces, followed by visual review.

### 2026-05-25

- Repo: frontend
- Changed: migrated budget surfaces — budget calculator list/empty states,
  budget chat, budget chat viewer, no-budget entry point and budget QA editor —
  from hardcoded blues, legacy `customActiveText`/`primary` aliases, old SVG
  gradient stops, loading indicators and budget action buttons to canonical
  `ht.*` classes or CSS-token SVG values.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted budget files now have no remaining matches for the migrated
  hardcoded brand-colour patterns. Remaining HT-008 work is admin and quiz
  surfaces, plus lower-priority miscellaneous surfaces, followed by visual
  review.

### 2026-05-25

- Repo: frontend
- Changed: migrated the first admin slice — admin protected route and article
  manager — from hardcoded app backgrounds, purple admin action colours, focus
  rings, loading indicators and blue metadata/action affordances to canonical
  `ht.*` classes or neutral Tailwind colours.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted admin article/protected-route files now have no remaining
  matches for the migrated hardcoded brand-colour patterns. Remaining HT-008
  work is knowledge-base admin, admin data/reporting, quiz and miscellaneous
  leftovers, followed by visual review.

### 2026-05-25

- Repo: frontend
- Changed: migrated admin data/reporting surfaces — admin data access and
  reporting dashboard — from hardcoded purple/blue chart colours, admin table
  links, sort indicators, period controls and chart strokes to canonical
  `ht.*` classes or token-backed chart values.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted admin data/reporting files now have no remaining matches for
  the migrated hardcoded brand-colour patterns. Remaining HT-008 work is
  knowledge-base admin, quiz and miscellaneous leftovers, followed by visual
  review.

### 2026-05-25

- Repo: frontend
- Changed: migrated `KnowledgeBaseAdmin.jsx` from hardcoded app backgrounds,
  purple admin actions, focus rings, loading indicators, document links,
  namespace badges and blue record counters to canonical `ht.*` classes or
  neutral Tailwind colours.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: `KnowledgeBaseAdmin.jsx` now has no remaining matches for the migrated
  hardcoded brand-colour patterns. The `_handlePreviewDocument` warning is left
  as a separate cleanup because this slice is limited to colour migration.
  Remaining HT-008 work is quiz and miscellaneous leftovers, followed by visual
  review.

### 2026-05-25

- Repo: frontend
- Changed: migrated quiz/onboarding surfaces — attitudinal quiz modal, quiz
  summary and complete-profile modal — from legacy active-state aliases,
  hardcoded range gradients, checked control colours and primary buttons to
  canonical `ht.*` classes or CSS-token values.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: targeted quiz/onboarding files now have no remaining matches for the
  migrated hardcoded brand-colour patterns. Remaining HT-008 work is
  miscellaneous leftovers, legacy alias cleanup and visual review.

### 2026-05-25

- Repo: frontend
- Changed: migrated miscellaneous leftovers — extension, resources, landing
  section tint, footer, arrow bullet, bookmark price, property detail links,
  popup dev-token link and one remaining Ask HomeTruth save-session link — then
  removed the unused legacy colour aliases from `tailwind.config.js`.
- Verification: `npm run build` completed successfully. The same existing
  unused-variable warnings remain in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`.
- Notes: the only remaining colour-regex matches are canonical token
  declarations in `src/index.css`; `Login.jsx` contains `#access_token`, which
  is an OAuth URL fragment and not a colour. Visual review remains open.

### 2026-05-25

- Repo: frontend
- Changed: no frontend code changes. Performed a browser visual smoke review of
  the token migration at `http://localhost:3001` for public/login surfaces:
  landing, pricing, login, admin login, guest chat, about, FAQ and Home Truths.
- Verification: public/login surfaces rendered without obvious colour-token
  regressions or layout breakage at the default desktop browser size. Protected
  user routes redirected to `/login`; protected admin routes redirected to
  `/admin/login`.
- Notes: `/home-truths` showed the expected empty-state UI but logged an Axios
  network error because no backend API was available for this local visual pass.
  The authenticated dashboard, documents, settings, quiz and admin content
  screens could not be visually reviewed without credentials or a purpose-built
  local visual harness, so the visual-review acceptance criterion remains open.

### 2026-05-25

- Repo: frontend
- Changed: no HT-008 code changes. Rechecked the remaining visual-review gap
  while progressing the design ticket queue.
- Verification: public landing/about/pricing smoke review still renders
  cleanly after the typography, gradient and icon changes.
- Notes: HT-008 remains open because its final acceptance criterion requires
  authenticated user/admin screens. Completion needs valid local credentials,
  seeded auth state or a dedicated visual harness for dashboard, documents,
  settings, quiz and admin content screens.

### 2026-05-25

- Repo: frontend
- Changed: added a gated local visual-review harness at `/visual-review`, enabled
  only when `REACT_APP_VISUAL_REVIEW=true`. The harness seeds user/admin auth
  state and mocked API responses so protected screens can be reviewed without
  live credentials or backend access.
- Verification: `REACT_APP_VISUAL_REVIEW=true npm run build` and `npm run build`
  completed successfully. Both builds still report the existing unused-variable
  warnings in `KnowledgeBaseAdmin.jsx` and `DataPrivacySettings.jsx`.
- Browser review: using the local visual harness at `http://localhost:3001`,
  reviewed dashboard, documents, Ask HomeTruth, quiz, account settings,
  preferences, notifications, data privacy, bookmarks, admin reporting
  dashboard, admin articles, knowledge base admin and admin data access. These
  authenticated screens rendered without access-denied states, backend-loading
  failures or visible colour-token/layout regressions at the default desktop
  browser size.
- Notes: this closes the final HT-008 acceptance criterion. The earlier public
  route visual review covered nav/header, auth and article/public surfaces.
