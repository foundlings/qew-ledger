id: 042cxmtk1
kind: issue
title: Add `qew start --take-over --reason` as a recorded takeover of another actor's claim
parent: 042cxmtjw
needs: 042cxmtjy 042cxmtjz
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: opppyqtx
---
## Behaviour
Taking over work another actor holds is a deliberate act. `qew start ITEM --take-over --reason TEXT` checks the item may start (not draft, no unmet needs, not completed or closed), then appends a forced `released` event (previous owner, reason, taker) and a `claimed` event for the caller, both in one command. Without the flag another actor's claim stays exit 3. Refused before any write: `--take-over` without `--reason` (2); nothing to take over because the item is unclaimed or the caller already holds it (2); an item that may not start (2), so the claim is never freed and then stranded.

## Scenarios
- golden: A holds, B takes over with a reason; events show forced release naming A then claimed by B (prevents: a takeover that leaves no record of whose claim was taken)
- plain start on A's claim still exits 3 naming `--take-over` (prevents: accidental takeover)
- no `--reason`: exit 2, zero events (prevents: unexplained takeover)
- unclaimed or own claim: exit 2 `nothing to take over`, zero events
- blocked or draft claimed item: refused before the release is written (prevents: freeing work and then failing to claim it)

## Reference coverage
5 reference test function(s): `test_start_still_refuses_another_logins_claim_without_take_over`, `test_start_take_over_moves_the_claim_and_records_whose_it_was`, `test_start_take_over_needs_a_reason_before_any_call`, `test_start_take_over_of_unclaimed_work_is_refused_without_writing`, `test_start_take_over_never_frees_work_that_may_not_start`

## Qew today
Missing. No `--take-over` flag, no forced release.
