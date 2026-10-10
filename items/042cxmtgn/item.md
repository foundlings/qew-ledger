id: 042cxmtgn
kind: issue
title: Report epic progress and completability from the ledger (campaign status)
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
In qew an epic is the campaign/milestone. Add counts to epic rows of `qew list --kind epic` / `qew show`: children open, children done, `completable` (not closed, at least one child, no open child), and the exact `qew complete EPIC` command only when completable. Terse text, JSON rows carry `schema_version`. Hostile titles are never echoed next to a runnable command: see `output-untrusted-text`. Closed epics are excluded from the default listing; a named epic shows even if closed.

## Scenarios
- `progress_distinguishes_completable_blocked_and_closed_epics`: three epics (all done, one open child, closed); JSON rows match exactly and only the first carries a command; prevents a wrong complete suggestion.
- `empty_epic_is_not_completable`: zero children never completable; prevents completing an empty plan.

## Reference coverage
Tests: campaign status distinguishes completable and blocked milestones (JSON rows). Docs: commands campaign status.

## Qew today
Missing. `qew list` has no counts; `qew complete` enforces the gate but nothing tells an agent which epics can be completed.
