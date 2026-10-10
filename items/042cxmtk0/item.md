id: 042cxmtk0
kind: issue
title: Make `qew complete` require the caller's own claim and refuse completed or unclaimed work
parent: 042cxmtjw
needs: 042cxmtjy
labels: area:lifecycle
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew complete` must refuse work the caller does not hold: claimed by another actor is exit 3 naming `--take-over` (see `take-over-complete`); unclaimed (approved) work is refused naming `qew start`; already completed work is refused with no second event, so a retry after a successful completion does not append a duplicate (the reference refuses a closed issue nobody claimed as exit 3 `no claim to complete`, never reports it done). Today `qew complete` checks only that the item is claimed, so any actor can complete another actor's claimed item.

## Scenarios
- another actor completes the claimed item: exit 3 naming the holder and `--take-over`, no event (prevents: completing work you do not hold)
- complete an approved, never-claimed item: refused, names `qew start` (prevents: skipping the claim step)
- retry after success: second complete refused as already completed, exactly one `completed` event (prevents: duplicate events after a lost response)
- golden: owner completes; owner cleared in the fold, item leaves `qew ready` and unblocks dependents (covered by test_golden_walk_claim_evidence_complete)

## Reference coverage
3 reference test function(s): `test_complete_golden_walk_closes_and_releases_claim`, `test_complete_seam_walk_refuses_work_not_claimed_by_caller`, `test_complete_refuses_closed_issue_the_caller_never_claimed`

## Qew today
Reduced. Golden path covered by flow walk test_golden_walk_claim_evidence_complete. No owner comparison anywhere in complete; a completed item is refused only through the generic state message and has no test. Forge-side auto-close reconciliation is dropped (see dropped).
