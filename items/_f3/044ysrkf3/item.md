id: 044ysrkf3
kind: epic
title: Write verbs read only the items they touch
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T19:28:00Z
---
## Problem

Every write verb that takes the ledger snapshot parses all 28,000 items under the write lock: 4 to 5 s idle, 17 to 24 s at load 30, so fifteen writers queue for minutes.

## Approach

docs/plans/lazy-item-snapshot.md: a lazy snapshot whose items, folds and events are read from the item's own files on first access, then a reverse-edge map for complete, then pr ready and open.

## Done when

evidence, start, complete and pr ready each show a lazy snapshot in their trace and a measured before and after on a clone of the foundlings ledger
