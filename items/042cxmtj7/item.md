id: 042cxmtj7
kind: issue
title: Make `qew hook remove` write nothing on a hook-free checkout, for every agent
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: wlskzyqr
---
## Behaviour
`qew hook remove` on a checkout with no agent config creates no file or directory (no `.claude`, `.codex`, `.cursor`, `.opencode/plugins`), exits 0 and prints `unchanged AGENT hook`, for each of the four agents and for the all-agents default.

## Scenarios
- Clean git checkout, remove per agent (4 subtests): directory listing identical before and after, stdout `unchanged AGENT hook`. Prevents a no-op removal littering the checkout with empty agent directories.

## Reference coverage
1 test (the reference hooks-remove-noop walk).

## Qew today
Reduced. The hook v1 walk checks `unchanged claude hook` after a second remove and the safe-write foundation says removal never creates directories, but no scenario lists the checkout before and after for all four agents.
