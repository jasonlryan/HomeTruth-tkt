# HT-004: Apply font-brand to all brand-facing components

**Priority:** P2
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Add font-brand class to headings and brand copy across all marketing/brand pages. Chat components keep font-chat.

## Files

- `src/components/Footer.jsx`
- `src/pages/AboutUs.jsx`
- `src/pages/Pricing.jsx`
- `src/components/FinalCTA.jsx`
- `src/components/WhoWeHelp.jsx`
- `src/components/TrustSecurity.jsx`
- `src/pages/Login.jsx`
- `src/pages/Register.jsx`
- `src/pages/WelcomePage.jsx`
- `src/pages/ComingSoon.jsx`

## Acceptance Criteria

- [x] All headings, navbar, footer, and marketing copy use Gill Sans
- [x] Chat bubbles and AI responses use system font
- [x] Visual distinction is clear

## Notes

Focus on h1, h2, h3, nav items, footer links, CTA text. Don't touch chat components.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: made brand typography explicit across the ticketed surfaces:
  footer, about, pricing, final CTA, who-we-help, trust/privacy, login,
  register, welcome and coming-soon surfaces now carry `font-brand` at the
  page/section/component level. CTA buttons now use `font-brand`. Chat remains
  isolated behind `font-chat`.
- Verification: `rg "font-sans|font-chat|font-brand" src/components src/pages`
  confirms brand-facing surfaces use `font-brand`, while the document chat
  surface still uses `font-chat`. `npm run build` completed successfully with
  the existing unused-variable warnings in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`, plus the existing outdated Browserslist notice.
  Browser smoke review covered landing, about and pricing.
