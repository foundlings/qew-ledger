id: 042cxmtkk
kind: issue
title: Refuse reserved label namespaces and unusable actor names on create and set
parent: 042cxmtjw
needs: 
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Sync replaces a mirrored issue's label set with the item's labels plus `qew:STATE`, `kind:KIND`, `priority:N`, and the reference derives an authorship label from the writer only. A caller-supplied label in a reserved namespace (`qew:*`, `kind:*`, `priority:*`, `author:*`, `in-progress`) would collide or forge authorship, so `create --label` and `set --add-label/--labels` refuse them (exit 2, before any write). The author of an item is derived from the first event's actor (`qew show` prints `author:`), never from a flag; an actor name that cannot form a mirror label (whitespace, comma, empty) is refused at the first write (today `QEW_ACTOR` is unvalidated and flows into events and mirror labels).

## Scenarios
- `--label author:mallory` and `--label qew:approved`: exit 2, zero files (prevents: forged authorship and state labels)
- actor `bad login,x`: create refused with exit 4 or 2, no item file (prevents: malformed text spliced into a label name)
- show prints the author from the first event; assignee is never used for authorship (prevents: author read as claim)

## Reference coverage
3 reference test function(s): `test_create_labels_work_with_the_author_who_opened_it`, `test_create_refuses_a_hand_written_author_area`, `test_create_refuses_a_viewer_login_that_cannot_be_a_label`

## Qew today
Reduced. Labels are checked only for whitespace and commas; no reserved namespaces; actor not validated. Authorship is implicit in event actors but not shown. Auto-creating a missing label (test_create_makes_a_missing_author_label_without_overwriting) is a forge-sync concern, see dropped.
