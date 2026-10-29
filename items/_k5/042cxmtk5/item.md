id: 042cxmtk5
kind: issue
title: Refuse a second lane under the same actor and report lane holders
parent: 042cxmtjw
needs: 042cxmtk4 042cxmtjx 042cxmtjz
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: opppyqtx
---
## Behaviour
Lane-aware start and release: a start on an item the caller already holds exits 3 naming the holding lane (or `without a lane`), also when `--lane` is omitted; it exits 5 only for the same lane, or for a lane-less start on a lane-less claim. Release of a lane claim by a different `--lane` is exit 3 unless `--force`. The lane guards `start` and `release` only; `complete`, `close`, `reopen` and `pr` do not check it (good-faith tooling, not access control; state this in the spec).

## Scenarios
- second lane, same actor: exit 3 naming lane A, no event (prevents: a sibling lane silently believing it owns work lane A holds)
- same lane again: exit 5, no event (prevents: duplicate claims on retry)
- lane start on a lane-less claim by you: exit 3 `without a lane`; lane-less start on a lane claim: exit 3 naming the lane; lane-less on lane-less: exit 5 (prevents: a loop reading exit 5 as `I hold it` for a sibling's claim)
- release naming the wrong lane: exit 3; with `--force`: succeeds and is recorded (prevents: freeing a sibling lane's work by accident)

## Reference coverage
5 reference test function(s): `test_second_lane_is_refused_and_named_without_writing`, `test_same_lane_again_keeps_already_claimed_by_you`, `test_lane_less_claim_by_you_refuses_a_lane_start`, `test_start_without_lane_on_a_lane_claim_names_the_lane`, `test_start_without_lane_on_your_lane_less_claim_keeps_exit_5`

## Qew today
Missing. Depends on lane data in the claimed event.
