# HomeTruth Ticket System

## Structure

```
.tickets/
├── README.md          ← You are here
├── open/              ← Active tickets ready to work on
├── deferred/          ← Parked tickets (blocked, low priority, or waiting on someone)
├── completed/         ← Done tickets (moved here, not deleted)
```

## Naming Convention

Each ticket is a markdown file named: `HT-NNN-short-description.md`

Example: `HT-005-standardise-cyan-hex.md`

## Numbering

| Range | Area |
|-------|------|
| HT-001 → HT-099 | Brand / Style |
| HT-100 → HT-199 | Frontend features |
| HT-200 → HT-299 | Backend features |
| HT-300 → HT-399 | Infrastructure / DevOps |
| HT-400 → HT-499 | Meeting prep / People / Process |

## Priority

Each ticket has a priority field:

| Priority | Meaning |
|----------|---------|
| P1 | Do now — blocking other work |
| P2 | Do next — important but not blocking |
| P3 | Do soon — nice to have, scheduled |
| P4 | Someday — parked, no urgency |

## Ticket Template

```markdown
# HT-NNN: Title

**Priority:** P1 / P2 / P3 / P4
**Repo:** frontend / backend / both / n/a
**Created:** YYYY-MM-DD
**Updated:** YYYY-MM-DD

## Description

What needs to happen.

## Files

- `path/to/relevant/file.js` — what to change

## Acceptance Criteria

- [ ] Criterion 1
- [ ] Criterion 2

## Notes

Any context, links, decisions.
```

## Workflow

1. New ticket → create in `open/`
2. Starting work → agent references ticket ID in commits
3. Blocked or parked → move to `deferred/`
4. Done → move to `completed/`

## For AI Agents

- Read `open/` to see what needs doing
- Pick highest priority (lowest P number) first
- Reference ticket ID in commit messages: `HT-005: standardise cyan hex`
- Update the ticket file with notes as you work
- Move to `completed/` when acceptance criteria are met
