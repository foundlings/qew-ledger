id: 042cxmti9
kind: issue
title: Report approved and remaining items when a multi-item draft move fails midway
parent: 042cxmti7
needs: 042cxmti8
labels: area:drafts-plans
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: xyslyokq
---
## Behaviour
Approve and revert write one event file per item. If a write fails after the first (disk error, permission, a
concurrent writer that took the same event id), the command exits 3 and prints `approved: ID...; not approved:
ID...; rerun the same command to finish`, plus `qew sync` as the way to refresh mirrors. Each written event is
read back (the folded state must be the intended one) and a mismatch is exit 3, never reported as success.
This mirrors the reference guarantee that a partial run is never left for the user to guess at. Because a rerun
skips items already moved (see draft-approve-targets), the printed advice is true.

## Scenarios
1. Fault injection: second event write fails in a three-item `--tree` approve; exit 3, stderr lists the approved and the not-approved ids and says to rerun, rerun finishes the rest. Prevents a half-released plan with no map of what is left.
2. Same walk for `draft revert`: stderr lists `reverted:` and `not reverted:`. Prevents a half-withheld plan.
3. Read-back mismatch: an appended event that folds to a different state (hand-planted illegal event file) is exit 3, not `approved`. Prevents reporting success for a move that did not take effect.
4. The failure message names `qew sync` as the mirror refresh. Prevents boards staying stale after a partial move.

## Reference coverage
Reference approve tests: failure after the first write lists what is left, partial failure names the board refresh,
edit that did not stick is reported (3 of 14). Reference revert tests: failure after the first write lists what is
left, edit that did not stick is reported (2 of 12). The failed-comment test (approve) has no ledger analogue: the
`approved` event itself carries the quote, so there is no second write that can be lost (see dropped).

## Qew today
Missing entirely: events are appended in a plain loop, any exception aborts with a traceback-free error but no list of what was and was not written; no read-back.
