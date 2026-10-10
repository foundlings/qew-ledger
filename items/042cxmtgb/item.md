id: 042cxmtgb
kind: issue
title: Derive the board column from ledger state with the reference's precedence rules
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
The column of an item on a target board is a pure function of the ledger snapshot (no network). Precedence, highest first: completed or closed -> Done (even if it was once a draft); draft -> Draft before every other rule; an epic is never Ready (it is not startable): it shows In progress while at least one open non-epic direct child is claimed, Done when completed/closed, Draft while a draft, otherwise it waits in Draft (qew has no Backlog column; record that decision in docs/specs/forges.md); approved, unclaimed, every need completed -> Ready; approved but blocked -> Draft (the column set is fixed at five); claimed -> In progress; claimed and an OPEN pull request mirror exists -> In review. A pull request mirror whose recorded state is merged or closed does NOT keep the item In review. The same function feeds `qew sync` and the planned offline `qew board`, so there is one implementation (`sync_plan.column`).

## Scenarios
- `golden_board_columns_follow_state`: walk one item through draft, approved, blocked, claimed, claimed+open PR, completed and assert the column at each step; prevents a drifting mapping between sync and board.
- `draft_with_approval_history_still_draft`: an item reverted to draft after being approved lands in Draft, not Ready; prevents a picked-up draft.
- `closed_or_completed_draft_is_done`: closed work never shows Draft/Ready; prevents stale cards.
- `epic_is_never_ready`: an approved unblocked epic is not offered as Ready on the board (`qew ready` excludes epics); prevents an unstartable card in the startable column.
- `epic_shows_in_progress_while_a_child_is_claimed`: derived epic status follows its children and returns when none is claimed; prevents a hand-set epic claim (qew never claims an epic).
- `merged_or_closed_pr_does_not_keep_in_review`: a pr mirror whose state is merged/closed lets the item fall back to In progress/Done; prevents a card stuck In review forever.

## Reference coverage
Tests: ready-state-and-priority projection, closed draft projects to Done, drafts project to the Draft column (three label shapes), approved-untriaged projects to Draft, plus the projections module's status precedence (closed, draft, epic, gate, review, claim, blockers). 4 tests map here directly; the gate-column tests are in the dropped list.

## Qew today
Covered: `sync_plan.column` handles Done/In progress/In review/Ready/Draft and tests/test_sync_walk.py `test_state_maps_to_open_closed_labels_and_columns` walks it. Missing: epic handling (an approved epic currently maps to Ready), pr mirror state (`_has_pull_request` ignores state), no dedicated column-derivation walk table, no spec text for the precedence. Offline `qew board` (planned separately) must call the same function and match every row above.
