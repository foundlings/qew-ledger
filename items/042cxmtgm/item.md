id: 042cxmtgm
kind: issue
title: Name the repair command when a board lacks a column or a sync step fails midway
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
When `place_on_board` finds the board has no column of that name (a board made before a column existed), the failure line must say how to repair it: 'board has no `Draft` column; run `qew project ensure`'. The same applies to a partial `qew draft approve` / `qew sync` failure: stderr lists what is left and ends with the command that refreshes the mirrors (`qew sync`), never a bare error. Exit codes unchanged; the offline work is not rolled back.

## Scenarios
- `sync_onto_a_board_without_the_draft_column_names_project_ensure`: failure text contains `qew project ensure`; prevents an opaque 'missing option' dead end.
- `partial_draft_approval_names_the_mirror_refresh`: failure after the first approval write names `qew sync`; prevents a user guessing how mirrors catch up.

## Reference coverage
Tests: a board without the draft column names project ensure (sync walk); partial failure names the board refresh (draft approve walk, board part only; the other 13 draft-approve tests belong to the drafts audit).

## Qew today
Reduced. forge_github raises `ForgeRejected(400, 'board has no `X` column ...')` with no repair hint; `draft approve` is ledger-only and never mentions sync.
