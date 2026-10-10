id: 042cxmtmx
kind: issue
title: Pin the ready/list/blocked text row and priority-then-id ordering
parent: 042cxmtmt
needs: 
labels: area:read-side
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Text rows are `ID STATE pN kind title [@owner]`, ordered by priority then by sortable id, identically for ready, list and blocked, so output order is deterministic across counter, letters and time id modes. The row must never contain control characters from an item title (see text-scan issues); the row for a long title is not truncated by ready but is bounded in prime.

## Scenarios
- golden: items at p3 and p0 created in the opposite order list p0 first in `ready`, `list` and `blocked`. Prevents agents picking low-priority work first.
- golden: same priority in counter id mode sorts numerically (2 before 10). Prevents lexicographic misorder.

## Reference coverage
Reference model-output walk `ready is priority sorted with typed vocabulary` (1 test).

## Qew today
Covered in substance by `ordered()` and `test_counter_mode_counts_up_and_lists_numerically`; ready-versus-blocked ordering equality is not asserted.
