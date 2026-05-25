# HomeTruth Tickets

This is the source-of-truth ticket repo for HomeTruth frontend and backend work.

The frontend and backend repos should reference ticket IDs from here; they should not contain ticket submodules or copied ticket trees.

## Ways of Working

This repo is the work ledger for the parallel HomeTruth build. Every codebase,
design-system, workflow, or documentation change must be traceable to a ticket
before it is started.

Use this rule:

```text
Ticket = why and what changed.
Commit = exact code change.
Design-system changelog = canonical brand/UI decision history.
```

For every change:

1. Create or select an open ticket before editing files.
2. Keep the ticket's affected repo field accurate: `frontend`, `backend`,
   `both`, `design-system`, or `n/a`.
3. State the ticket goal and acceptance criteria clearly enough that someone
   else can tell when the work is done.
4. Reference the ticket ID in branch names, commit messages, pull requests, and
   implementation notes.
5. Add an `Implementation Log` entry to the ticket before moving it to
   `completed/`.
6. For design-system changes, also update `../design-system/CHANGELOG.md`.

Suggested ticket shape:

```markdown
# HT-NNN: Title

**Priority:** P1 / P2 / P3 / P4
**Repo:** frontend / backend / both / design-system / n/a
**Created:** YYYY-MM-DD
**Updated:** YYYY-MM-DD

## Goal

The outcome this ticket must achieve.

## Description

Useful context, constraints, and why the change matters.

## Files

- `path/to/file` — expected change

## Acceptance Criteria

- [ ] Observable result or verification point
- [ ] Observable result or verification point
```

Suggested implementation log format:

```markdown
## Implementation Log

### YYYY-MM-DD
- Repo: frontend / backend / design-system / both / n/a
- Changed: short summary of files or behaviour changed
- Verification: tests, build, review, or reason not run
- Notes: decisions, tradeoffs, or follow-up risks
```

## Structure

```text
open/       Active tickets ready to work on
deferred/   Parked tickets that are blocked, lower priority, or waiting on someone
completed/  Finished tickets moved here rather than deleted
```

## Workflow

1. Create and update tickets in this repo.
2. Reference ticket IDs in branch names, commit messages, pull requests, and implementation notes.
3. Move tickets from `open/` to `completed/` when acceptance criteria are met.
4. Move tickets to `deferred/` when they are intentionally parked.

Example commit message:

```text
HT-005: standardise cyan hex usage
```
