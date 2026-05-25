# HT-010: Add building block icon SVGs

**Priority:** P4
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Source or create SVG versions of the building block icons from the brand style guide (p13). Add as React components. These are geometric overlapping coloured squares used as framing elements and feature indicators.

## Files

- `src/components/icons/BuildingBlockIcon.jsx`
- `design-system/icons/icon-lifecycle-*.svg`

## Acceptance Criteria

- [x] SVG components for building block icons in brand colours
- [x] Usable as framing elements on feature cards, Trust & Security section,
  Who We Help section

## Notes

Style guide rule: building block icons on white or black backgrounds only — not over images. Four lifecycle stage icons: Purchase, Maintain, Improve, Sell. Each uses a different colour combination.

## Implementation Log

### 2026-05-25

- Repos: frontend, design-system
- Changed: added a token-backed `BuildingBlockIcon` React component with
  `purchase`, `maintain`, `improve` and `sell` variants. Added the canonical
  lifecycle SVG motifs to the design-system `icons/` folder. Used the icon
  component as framing on the Who We Help and Trust & Privacy sections.
- Verification: landing page browser smoke review shows the building-block
  motif renders on white/gray content surfaces and avoids image overlays.
  `npm run build` completed successfully with the existing warnings.
