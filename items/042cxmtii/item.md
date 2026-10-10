id: 042cxmtii
kind: issue
title: Refuse dependency and parent writes that create cycles, self edges, dangling refs or bad nesting
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: wusmzrpq kmrvrqzl
---
## Behaviour
Reference graph invariant: an edge is validated against the complete graph before it is written, and a bad edge
never reaches storage. In qew `create` and `set` write `needs`/`parent` unchecked and `qew check` only reports the
damage afterwards (the existing check walk creates a cycle with `set --needs` and then expects `check` to fail).
Required before any file write, exit 2:
- self edge (`needs` or `parent` equal to the item), unknown reference, duplicate entries in `needs`;
- a `needs` or `parent` change that closes a cycle through existing items (transitive), message names the cycle;
- a parent whose kind may not hold the child (epic > issue > task, task directly under epic) including `set --kind`
  style changes that would orphan the existing nesting;
- editing a closed item is refused unless `--closed` is passed explicitly (as the reference does for `set`, `block`,
  `unblock`); the audit `field` event is written together with the header change and a read-back verifies it.
`qew check` keeps reporting the same problems for hand-merged files.

## Scenarios
1. `set A --needs B` where B already needs A: exit 2 `cycle`, neither file changed. Prevents a cycle reaching storage.
2. Longer transitive cycle A needs B, B needs C, set C needs A refused. Prevents indirect cycles.
3. Self need / self parent refused; unknown reference refused; duplicate need refused. Prevents malformed edges.
4. Task under a task, issue under an issue, epic under anything refused at `create` and `set`. Prevents nesting that `check` would later fail.
5. `set` on a closed item exit 2 `closed; pass --closed`; with `--closed` it applies. Prevents stale edits of finished work by accident.
6. Failed validation leaves no `field` event. Prevents an audit trail for a change that never happened.

## Reference coverage
Reference graph-write tests merged: block refuses a transitive cycle before write (1), set rejects a closed target
without override (1); also the plan-status/graph decode loud failure on truncated or malformed data (maps to
`qew check` and every read failing loudly on malformed files, already true). 2 of 26 graph-write tests.

## Qew today
Reduced: only parse-time header checks (valid ids, kinds, no self-need on check). No pre-write cycle, kind-nesting, unknown or closed-target validation in `create`/`set`.
