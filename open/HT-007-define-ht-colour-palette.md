# HT-007: Define ht-* colour palette in tailwind config

**Priority:** P1
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-03-29

## Description

Add a proper ht.* colour namespace in tailwind.config.js. Remove off-brand colours that don't appear in the style guide.

## Files

- `tailwind.config.js` — lines 14-31

## Acceptance Criteria

- [ ] tailwind config has ht.cyan, ht.cyan-hover, ht.orange, ht.orange-hover, ht.purple, ht.green, ht.navy, ht.black, ht.grey, ht.grey-light
- [ ] Off-brand colours removed: primary (#4A6BFF), myblue (#2960EC), softBlue (#7098FE), blurpleLight (#859BFF), customBlue (#E6ECFF)

## Notes

Keep textClor (#333333 — note the typo), darkGrey, lightGrey, smoke, bgColor as they may be used for UI chrome. Fix the textClor typo to textColor while at it.
