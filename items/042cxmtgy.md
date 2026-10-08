id: 042cxmtgy
kind: issue
title: Pin that board, selection and limits never leak from one mirror target to another
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
The reference had to fix a bug where its single checkout-wide mode, board link and claim cap were applied to a foreign `--repo` (a backfill wanted 1154 issues instead of 310; 1916 foreign cards on one board). Qew's per-target model prevents this structurally (`boards/<slug>.json`, per-mirror `select`, `project`), so only walks are needed to keep it so: (1) two targets with different repos each use their own recorded board id; (2) a target without `select` mirrors all items but a `select` on another target is never applied to it; (3) `qew project ensure --target B` never writes `boards/A.json`; (4) a code-repo-wide limit such as a future claim cap in `[code]` is read from the code repo config and never from a mirror's repository; (5) a repository URL that differs only in case or `.git` suffix is the same target (casefolded slug), so a board is not duplicated.

## Scenarios
- `two_targets_use_their_own_boards`: ensure on both creates two records; sync places on the right board each; prevents cross-writing.
- `select_is_per_target`: sync to B ignores A's expression.
- `ensure_target_b_does_not_touch_target_a_record`: file hash of A unchanged.
- `case_and_git_suffix_variants_are_one_target`: `Acme/Widgets.git` and `acme/widgets` share a slug; prevents duplicate boards.

## Reference coverage
Tests: foreign repository mode walk (4: foreign repository scoped to managed issues, checkout's own repository keeps its mode, unreadable origin keeps mode, claim cap never applies to another repository); project link repository walk (5: another repository does not use the link, selects by title, own repository still uses it with three remote spellings, a mutation for another repository syncs no card, unreadable origin keeps the link).

## Qew today
Structural, mostly covered: tests/test_sync_walk.py `test_golden_walk_mirrors_per_target...`, tests/test_sync_cli_walk.py target filter. Missing: case/.git slug normalisation (`mirror_slug` does not casefold or strip `.git`) and a board-record isolation walk.
