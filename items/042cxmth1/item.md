id: 042cxmth1
kind: issue
title: Keep forge-side admin commands out of the CLI and refuse them in the hook guard
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: zzuwzrzw
---
## Behaviour
The reference had `adopt`, `author backfill`, `area ensure`, `project prune` and mode flags because a forge was the store. Qew must not grow lookalikes. Pin by a walk that `qew --help` lists none of `adopt`, `author`, `area`, `campaign` (the replacements are `qew sync`, derived author, header labels, epics) and that the hook guard still refuses direct forge label, milestone, board and project edits with advice naming the qew command to use instead. (Existing guard: hook_guard `_MILESTONE_ADVICE`.)

## Scenarios
- `help_lists_no_forge_as_store_commands`: prevents scope creep back into forge-as-store admin.
- `hook_refuses_forge_label_and_board_edits_with_qew_advice`: refusal text names `qew sync`/`qew project ensure`.

## Reference coverage
Guard rails for the dropped commands above; no reference test maps one to one.

## Qew today
Hook guard already covers label/milestone/board edits (tests/test_hook_v1_walk.py); the help assertion is new.
