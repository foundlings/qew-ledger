id: 042cxmtkh
kind: issue
title: Validate parent and needs edges before any write on create, set and block
parent: 042cxmtjw
needs: 
labels: area:lifecycle
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: wusmzrpq
---
## Behaviour
One shared validator for every command that writes an edge. Before a file or event is written: referenced items exist, no self edge, the new `needs` graph has no cycle (including through the new item), the parent kind hierarchy holds (epic > issue > task, task directly under epic allowed; `qew check` enforces it today but create and set do not), and priority is a non-negative integer. Today `qew set --needs X` or `--parent Y` writes first and only `qew check` finds a cycle or illegal parent afterwards, leaving a broken ledger committed to a shared branch.

## Scenarios
- set needs creating a cycle: exit 2 naming the cycle, item file and events unchanged (prevents: broken ledger pushed by a single command)
- set parent to a task or to a lower kind: exit 2 naming the rule (prevents: illegal hierarchy)
- create with unknown parent or need, and `--from-file` with an `@ref` cycle: exit 2 and no file written at all (prevents: half-created batches)
- set with no change: `unchanged`, exit 0, no event (covered by existing set walk partly)

## Reference coverage
No dedicated reference test; specified from the reference command documentation. (spec) shared validator for graph writes; tests above are the reference's block, set and create refusals

## Qew today
Reduced. create resolves refs but never checks cycles or parent kind; set resolves ids but never checks.
