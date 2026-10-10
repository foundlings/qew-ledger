id: 042cxmtkg
kind: issue
title: Complete an epic automatically when its last open child finishes
parent: 042cxmtjw
needs: 042cxmtkf
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
When `qew complete` or `qew close` finishes the last open child of an epic, qew appends the epic's `completed` event in the same command (actor recorded, reason `all N children finished`) provided the epic is open, has at least one child, and every child is completed or closed. An epic with any open child is never auto-completed; an epic nobody claimed still completes (no explicit claim needed). The child event is written first, so a failure of the epic step leaves the child done and prints a warning naming the explicit `qew complete EPIC`, exit 0, never failing the user's command. `qew complete EPIC` stays as the explicit path.

## Scenarios
- last child completes: epic completes with an all-children reason; parent chain completes upward only when its own children are done (prevents: epics left open forever)
- an open child remains: epic untouched (prevents: premature epic completion)
- epic step fails (write error): child stays completed, exit 0 with a warning naming the explicit command (prevents: a successful child completion reported as failed, inviting a retry)
- epic with only closed (not planned) children: completes only if at least one child completed or the spec says otherwise (prevents: completing an epic that delivered nothing)

## Reference coverage
5 reference test function(s): `test_closing_the_last_open_child_completes_the_epic`, `test_an_epic_with_an_open_child_is_never_auto_completed`, `test_a_failing_reconcile_only_warns_and_never_fails_the_command`, `test_a_failing_auto_completion_only_warns`, `test_an_epic_without_a_single_priority_is_never_auto_completed`

## Qew today
Missing. Epic completion is explicit only. The single-priority guard is a GitHub label concept; qew has one priority header field by construction (dropped part).
