id: 042cxmtki
kind: issue
title: Add `qew block` and `qew unblock` for dependency edges
parent: 042cxmtjw
needs: 042cxmtkh
labels: area:lifecycle
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew block ITEM --on DEP` adds DEP to ITEM's `needs`; `qew unblock ITEM --from DEP` removes it. Each is idempotent (an existing or absent edge is `unchanged`, exit 0), appends a `field` audit event with old and new needs, and refuses before any write: a self edge, an unknown item, a transitive cycle (names the cycle), and a completed or closed ITEM unless `--closed` (the reference demands the override to protect finished work). Today only `qew set --needs` exists, which replaces the whole list, so an edge add from a stale view silently drops a concurrently added edge.

## Scenarios
- golden block: edge added, `qew blocked` and `qew graph` show it, audit event written (prevents: an edge that is not visible or not audited)
- transitive cycle (A needs B, then block B on A): exit 2 naming the cycle, zero writes (prevents: deadlocked graph)
- closed/completed target without `--closed`: exit 2 naming the flag (prevents: editing finished work by accident); with `--closed` unblock succeeds
- golden unblock removes the edge, item becomes ready; repeating it is `unchanged` (prevents: errors on retry)
- two branches each add a different edge via block: merge keeps both because each edge is its own event (prevents: lost edge from replace-the-list editing)

## Reference coverage
5 reference test function(s): `test_block_golden_walk_adds_and_verifies_edge`, `test_block_seam_walk_refuses_transitive_cycle_before_write`, `test_unblock_golden_walk_removes_and_verifies_edge`, `test_block_refusal_walk_requires_closed_override`, `test_unblock_golden_walk_allows_explicit_closed_target`

## Qew today
Missing. Only `qew set --needs` (full replace) exists; `qew check` finds cycles after the fact.
