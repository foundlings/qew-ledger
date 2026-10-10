id: 042cxmtgg
kind: issue
title: Add `qew project status`: a read-only drift report of the board against the ledger
parent: 042cxmt4m
needs: 042cxmtgf 042cxmtgb
labels: area:board-admin
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew project status [--target T] [--json]` compares, per target, the derived column (and Priority) of every selected item with the live card and prints: `<slug>: in sync` or the drift lists `missing`, `stale_column`, `stale_priority` plus the one fix command `qew project ensure` / `qew sync`. It never writes. Exit 0 when in sync, 1 when drifted or the forge fails, 2 on a bad target; a target without a recorded/configured board says so and names `qew project ensure` (exit 2); an Unsupported forge prints 'boards unsupported' like ensure. JSON rows carry `schema_version`, `in_sync`, `missing`, `stale_column`, `stale_priority`, `fix`. Drift is advisory: forge state is never read back as truth for the ledger (sync stays push-only); the report only says the forge disagrees.

## Scenarios
- `status_reports_missing_and_stale_cards_without_writing`: board lacks one item and holds another in the wrong column; JSON lists both, no mutation issued; prevents silent unmirrored work.
- `status_reports_in_sync_in_one_line`: nothing drifted prints the single in-sync line, exit 0; prevents noisy output for agents.
- `status_refuses_a_missing_board_without_writing`: no board recorded and none configured: refusal names `qew project ensure`; prevents guessing a board.
- `status_uses_the_recorded_board_without_flags`: boards/<slug>.json supplies the board; prevents requiring a title on every call.
- `status_on_a_forge_without_boards_says_so`: Forgejo target prints 'boards unsupported', exit 0; prevents a false failure.

## Reference coverage
Tests: status reports missing and stale items without writing, uses the linked project, reports in sync when nothing drifted, refuses a missing project without writing (4 tests) plus the overlap/foreign-card tests (in `board-card-reading-and-duplicates`).

## Qew today
Missing: no `project status`. The planned offline `qew board` must produce the same `missing`/`stale` vocabulary when run against recorded mirrors; keep JSON field names identical.
