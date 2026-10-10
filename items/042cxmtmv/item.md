id: 042cxmtmv
kind: issue
title: Bound `qew ready` with a default limit, --limit 0 for all, and truncation reporting
parent: 042cxmtmt
needs: 042cxmtmu
labels: area:read-side
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: tyqqmllz
---
## Behaviour
`qew ready` returns at most 30 items by default in priority order (lower number first, then stable id order), reports `total` and `truncated`, and warns on stderr when it truncated. `--limit N` changes the bound; `--limit 0` returns everything. The bound exists so an agent session never silently swallows a 500-item ready list. Negative or non-integer limits are a usage error (exit 2).

## Scenarios
- golden: 31 ready items, default run prints 30, `total` is 31, `truncated` is true and stderr says so. Prevents agent context growing without bound.
- golden: `--limit 0` on the same ledger prints all 31, `truncated` false. Prevents a caller that wants everything being capped.
- refusal: `--limit -1` and `--limit abc` exit 2 before reading the ledger. Prevents a nonsense bound slicing the list from the wrong end.

## Reference coverage
Reference ready walk: default limit bounded and reports truncation; zero limit returns all (2 tests).

## Qew today
Missing. `qew ready` prints every ready item with no limit, total or truncation signal.
