id: 042cxmtge
kind: issue
title: Select the target board by recorded number and refuse conflicts instead of guessing
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
A mirror's `project` is a positive integer (board number), accepted from the config or from `boards/<target>.json`. It survives a board rename. Validation happens at config load, before any network call: a title string, a numeric string used as a title, 0, a negative number, a boolean or a float is refused (exit 1/2, message 'project must be a positive board number'). A number that no board has is refused WITHOUT creating a new board (the checkout would silently drift). When `project_title` is also given and differs from the linked board's current title, refuse with a conflict naming both (never reconcile a different board). A target with neither `project` nor a recorded board creates one titled by `project_title`, default the repo name (qew's deliberate difference from the reference, which demands a title); an empty `project_title` is refused.

## Scenarios
- `linked_board_found_by_number_after_a_rename`: board renamed on the forge is still found and ensure reports its new title; prevents a silent unlink.
- `missing_board_number_is_refused_without_creating`: number 99 absent: exit non-zero, no create mutation issued; prevents drift to a new board.
- `title_option_conflicting_with_linked_number_is_refused`: refusal names both the number and the actual title; prevents reconciling the wrong board.
- `non_positive_or_mistyped_project_is_refused_at_load`: table of bad values refused before any request; prevents a title masquerading as a number.
- `empty_project_title_is_refused`: blank title never creates an unnamed board.

## Reference coverage
Tests: project commands refuse a title that conflicts with the linked project (ensure and status), find the linked board by number after a rename, a linked board that does not exist is refused without creating one, a project command without any title is refused, config refuses a project that is not a positive number, sync finds the board by number after a rename (6 tests, one table-driven over six bad values).

## Qew today
Partly covered: `test_unknown_project_number_is_rejected` and `test_board_id_round_trips_as_the_mirror_project` (GitHub), GitLab round trip tests. Missing: positive-integer validation (`ledger_config._mirror` does `str(project)` on anything), the title-versus-number conflict refusal, and the empty-title refusal.
