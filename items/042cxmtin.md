id: 042cxmtin
kind: issue
title: Add `qew plan status [EPIC]` with a deterministic child rollup and next ready child
parent: 042cxmti7
needs: 042cxmtie
labels: area:drafts-plans status:Backlog
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew plan status [EPIC] [--json]` rolls up the direct children of one epic, or of every open epic when none is
named, from files only. Counts: `total`, `draft`, `ready`, `blocked`, `claimed`, `closed` (completed or closed).
`next` is the highest-priority ready child (lowest priority number, then id) with reason
`highest-priority ready child`; drafts and blocked children are never selected. `completable` is true only for a
non-draft epic with at least one child and every child completed or closed; then `complete_command` is
`qew complete ID` (the ledger has no separate plan-complete verb) otherwise null. A draft epic reports
`draft: true`, is never completable and prints `(draft plan)`. Text first line: `ID state title` then
`N/M closed` with `, K drafts` only when K > 0. A named item that is not an epic, or an unknown id, is exit 2.
Unreadable data (dangling need, illegal event order) fails loudly, never a guessed count.
Update help, README and the commands spec together.

## Scenarios
1. Golden rollup with one closed, one claimed, one blocked, two ready (P1, P2) and a draft: counts exact, next is the P1 child, JSON shape fixed (`schema_version` 1). Prevents derived state living in prose.
2. A draft child with the best priority is counted as draft and never selected as next. Prevents drafts leaking into next-work advice.
3. Every child completed: `completable` true and `complete_command` names the ledger command. Prevents agents guessing the closing step.
4. Draft epic whose children are all done: `draft` true, not completable, text says draft plan. Prevents offering a command that will refuse.
5. Text output: `0/3 closed, 2 drafts`; without drafts exactly `0/1 closed`. Prevents a reader mistaking drafts for live work.
6. Child with a dangling need or a child file that fails to parse: exit non-zero, no rollup. Prevents guessing a ready state from partial data.
7. No argument lists every open epic; a non-epic id or unknown id exit 2. Prevents a rollup of a task as if it were a plan.

## Reference coverage
Reference plan-status tests: golden rollup and next ready work, approval-gated children counted (dropped; no ledger
analogue), completion command named when every child is closed, seam refusing incomplete child dependencies
(truncation maps to loud failure on malformed data) - 4 of 6 (golden, command, seam, gate dropped); draft-state test
plan status counts a draft child; draft-text tests plan status counts drafts in text, draft plan never completable,
text unchanged without drafts - 4 more (8 reference test functions in total fold here, counted by the
primary file once).

## Qew today
Missing: there is no plan command; `show` lists children but no rollup, no next ready child.
