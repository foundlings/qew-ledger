id: 042cxmtgk
kind: issue
title: Make `qew sync --item` refresh the cards its change moves (dependents and the parent epic)
parent: 042cxmt4m
needs: 042cxmtgb
labels: area:board-admin
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
A card's column depends on other items: completing or closing a need moves its dependents from Draft to Ready; claiming or releasing a child moves the parent epic card. `qew sync --item ID` (and `--dry-run --item`) must therefore also place the cards of items whose derived column changed because of ID, not only ID's own card. Each affected card is written once and only when its column differs. A full `qew sync` already covers all items; the gap is the targeted form.

## Scenarios
- `completing_a_need_moves_its_dependent_to_ready`: sync --item NEED places NEED in Done and dependent in Ready; prevents dependents stuck in Draft.
- `claiming_a_child_moves_the_epic_card`: epic card moves to In progress and back on release; prevents a stale epic.
- `unchanged_cards_are_not_rewritten`: second targeted sync issues no board write.

## Reference coverage
Tests: complete also moves the cards of issues it unblocks (two status writes in order), start moves the claimed card to In progress; spec: targeted card sync after mutations.

## Qew today
Reduced. `sync_target` with `only` skips every other item (`chosen` filter), so targeted sync leaves dependents stale. `test_boards_get_the_column_for_the_state...` covers the single-card move only.
