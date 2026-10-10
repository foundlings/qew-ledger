id: 042cxmtgd
kind: issue
title: Mirror item priority to a board Priority field and keep it current
parent: 042cxmt4m
needs: 042cxmtgc
labels: area:board-admin
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Boards carry a second single-select field, Priority, with options P0..P4 (ledger `priority: N`, lower is sooner). `project ensure` creates or repairs it with the same keep-foreign-options rule as Status; `place_on_board` (or a new `set_board_priority`) writes only the values that differ; a priority change in the ledger moves the card's Priority on the next sync. A priority outside the board's options is a typed rejection before any write. Forges without fields skip it as Unsupported.

## Scenarios
- `sync_creates_card_with_priority_and_status`: a new approved item lands with Status Ready and Priority from the header in the expected writes; prevents unprioritised boards.
- `priority_change_updates_only_the_priority_field`: `qew set --priority` then sync writes Priority once and leaves Status untouched; prevents status churn.
- `unknown_priority_option_is_rejected_before_any_write`: priority 9 on a P0..P4 board is a typed error; prevents a half-written card.

## Reference coverage
Tests: ready-state-and-priority projection (item, priority and status writes), create adds the card with priority and status, status reports stale priority. Spec: projects.md Priority field.

## Qew today
Missing. Board has only Status; `Board` carries no fields; the item header priority reaches the forge only as the `priority:N` label.
