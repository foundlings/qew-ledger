id: 042cxmtic
kind: issue
title: Refuse to revert claimed work or work under review, naming `qew release`
parent: 042cxmti7
needs: 042cxmtib
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Pulling work from under its claimant is the accident the reference guards against and there is deliberately no
force flag. In the ledger model:
- Claimed state (any owner, epics included) refuses the revert with exit 3 and the message `ID is claimed by
  OWNER; release it first with qew release ITEM, nothing was changed` (today the generic transition text
  `cannot reverted an item that is claimed` exits 2 and does not name the way out).
- Work that has an open, non-draft pull request mirror (`mirrors/<ID>/<target>-pr-<N>.json`, kind pr, not
  recorded as draft) is refused exit 2 `has an open pull request; close or merge it first`. A draft pull
  request (for example a plan's epic pull request) is not review and does not block.
- With `--tree`, one claimed or in-review descendant refuses the whole tree before any event is written, naming
  that descendant.
- A reverted plan stops being claimable; children of a reverted epic stay as they are.

## Scenarios
1. Claimed item refused, exit 3, message contains `qew release`, no events appended. Prevents silently taking work from a claimant.
2. Claimed epic refused the same way. Prevents withdrawing a plan someone is driving.
3. `--tree` where only the second descendant is claimed: refuses everything and names it; first descendant untouched. Prevents a half-reverted tree.
4. Approved item with an open ready pull request mirror refused; with a draft pull request mirror accepted. Prevents withdrawing work already in review.
5. After `qew release` the same revert succeeds. Prevents a dead-end workflow.

## Reference coverage
Reference revert tests: claimed work refused and names the holder (assignee and in-progress variants), one claimed
descendant refuses the whole tree, epic with a derived claim refused, work in review refused (4 of 12). Assignee and
in-progress label variants collapse to the single claimed state in the ledger.

## Qew today
Reduced: claimed work is refused through the state machine at exit 2 with no hint; no pull request mirror check; no tree mode to refuse.
