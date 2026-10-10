id: 042cxmtgh
kind: issue
title: Add `qew project prune --from OWNER/REPO` to remove another repository's cards from a shared board
parent: 042cxmt4m
needs: 042cxmtgf
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Two mirror targets may point at one organization board. `qew project prune --target T --from OWNER/REPO` deletes exactly the cards whose issue belongs to the named repository (exact, case-insensitive match; never a prefix such as acme/other-two), then re-reads and fails with an indeterminate error if any remain. Refuses before any call: a malformed source (`other`, `a/b/c`, empty, spaces) and the target's own repository. Deleting a card never touches an issue. Nothing to remove prints `removed 0` and issues no delete. Forge Board interface gains `remove_from_board(board, card)`; Unsupported elsewhere.

## Scenarios
- `prune_deletes_exactly_the_named_repositorys_cards_and_verifies`: five cards, two foreign: only those two deleted, re-read confirms; prevents deleting the board's own or a look-alike repository.
- `prune_refuses_the_boards_own_repository_before_any_call`: prevents emptying the target's own board.
- `prune_refuses_malformed_sources_before_any_call`: table of four malformed values; prevents a loose match.
- `prune_with_nothing_to_remove_deletes_nothing`: idempotent no-op.
- `cards_that_remain_after_deletes_are_indeterminate`: a delete that did not stick is reported, not success.

## Reference coverage
Tests (project prune walk, 5): deletes exactly the named repository's cards and verifies, own repository refused, malformed source refused, nothing to remove, cards that remain are indeterminate.

## Qew today
Missing. Low priority because qew boards are keyed per target; becomes real when two targets share one board.
