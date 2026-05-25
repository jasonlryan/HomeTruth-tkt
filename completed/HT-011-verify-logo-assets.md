# HT-011: Verify logo assets match current brand guide

**Priority:** P3
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Check that logo.png and HOME_TRUTH_POS_F PNG files match the TH square icon in the style guide. Consider replacing with SVG for sharper rendering.

## Files

- `public/assets/logo.png`
- `public/assets/HOME_TRUTH_POS_F 2 (3).png`
- Referenced in: `Navbar.jsx:32`, `Footer.jsx:62`, `Sidebar.jsx:31`, `ComingSoonHeader.jsx:9`, `Login.jsx:148`, `AdminLogin.jsx:111`, `Register.jsx:94`, `WelcomePage.jsx:68`

## Acceptance Criteria

- [x] Logo files confirmed as current or replaced with updated versions
- [x] SVG option evaluated

## Notes

Style guide p7 has annotation "Change purple throughout" — the purple in the TH icon may be changing.

## Implementation Log

### 2026-05-25

- Repos: frontend, design-system
- Changed: no frontend logo replacement needed. Audited the active logo
  references and compared them with the design-system logo assets. The active
  frontend full-colour wordmark uses the same HomeTruth lock-up as the
  design-system PNG logo, and the design-system contains an SVG master for the
  TH icon.
- Verification: active frontend logo references are `public/assets/logo.png`
  and `public/assets/HOME_TRUTH_POS_F 2 (3).png`. `file`, `sips`, `shasum` and
  visual inspection confirmed the raster assets are valid PNGs and match the
  current tracked lock-up. SVG option evaluated: an SVG exists for the TH icon
  (`design-system/logos/hometruth-icon.svg`), but no full wordmark SVG is
  available in the tracked assets. Full wordmark replacement should wait for an
  official vector wordmark.
- Notes: the p7 purple-change annotation remains tied to HT-012 external brand
  confirmation. If BrandAd changes the purple, update design-system tokens and
  regenerate logo/icon assets in a follow-up ticket.
