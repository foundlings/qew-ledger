id: 042cxmtmf
kind: issue
title: Enforce PR ownership: opener or holder of every covered claim, with `--other-author --reason`
parent: 042cxmtm4
needs: 042cxmtm9 042cxmtmb
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
## Behaviour
`ready`, `merge` and `check` act only on a PR the caller opened, or whose covered items the caller holds ALL claims on (claims derived from `claimed`/`released` events; the lane building a plan holds its integration item while the planner opened the PR). Otherwise exit 3 naming the opener and both ways forward: take over the items (`qew start ITEM --take-over --reason TEXT`) or, for merge only, `--other-author --reason TEXT`. `--other-author` requires `--reason` (exit 2 before any call), prints `merging LOGIN's pull request: REASON`, and NEVER overrides readiness rules. A PR that covers no item, an unclaimed item, an item claimed by someone else, or only some claimed all refuse. The covered items come from the ledger pr mirror, not from forge text.

## Scenarios
- teammate PR, caller holds every claim: ready, check and merge proceed. Prevents: needing the original author to be online.
- refusal table: unclaimed, claimed by another, one of two claimed, covers nothing: exit 3 text names opener, `--take-over` and (merge) `--other-author`, zero writes. Prevents: acting on a teammate's PR by accident.
- other author for ready and check: refused, no override flag (only merge has one). Prevents: privilege creep.
- `--other-author` with reason merges and prints the reason; without reason exit 2 and zero calls; draft PR still refused with it. Prevents: using the override to skip readiness.
- indeterminate claim data (corrupt events) fails loudly exit 4, never guesses owner. Prevents: wrong-owner merges.

## Reference coverage
Reference owner module (author or all-claims check) used by ready (3 tests), check (3 tests), merge (3 tests) in their walk files. 9 test functions mapped here.

## Qew today
Missing: qew has no `--take-over`, no `--other-author`, no opener on the pr mirror, no ownership check at all in cmd_pr. Depends on a claim take-over feature in the claim area.
