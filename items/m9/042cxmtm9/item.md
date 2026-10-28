id: 042cxmtm9
kind: issue
title: Record the PR opener in the pr mirror and require claim or opener for open
parent: 042cxmtm4
needs: 042cxmtm5
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
## Behaviour
`qew pr open` for an approved item requires the caller to hold the item's claim (derived from events), or the item to be draft. The pr mirror records `opener` (actor login) and the item ids it covers, so later `ready`/`merge`/`check` can apply the ownership rule (see pr-owner-rule).

## Scenarios
- unclaimed approved item: `qew pr open` refused with a hint to `qew start`, nothing opened. Prevents: PRs for work nobody owns.
- item claimed by someone else: refused naming the owner. Prevents: a lane hijacking another lane's PR.

## Reference coverage
Reference lifecycle rule that pr requires the caller's claim, plus the owner assignment test in the lifecycle walk file (1 test function, folded into pr-open-golden).

## Qew today
Missing: `open_pull_request` checks only the item state, never the claim; the pr mirror stores no opener or covered items.
