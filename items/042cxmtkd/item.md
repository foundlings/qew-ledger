id: 042cxmtkd
kind: issue
title: Close work delivered by someone else with a landing proof
parent: 042cxmtjw
needs: 042cxmtkc 042cxmtk2
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
When a commit that nobody claimed delivered an item, the reference lets `close --delivered-by SHA --landed-on BRANCH` record it as completed with the same landing proof as `complete`; half a proof (one flag), or an unlanded commit, is refused before any write. In qew the `completed` state needs a claim; add a close disposition `delivered` (or allow `qew complete --deliverer` from approved) that requires landed evidence, stores it and reaches `completed` so dependents unblock. Without it, work shipped outside qew can only be closed as not planned, which wrongly keeps dependents blocked.

## Scenarios
- golden: unclaimed approved item, delivered-by commit on target; item is completed, evidence stored, dependents become ready (prevents: dependents blocked forever behind externally shipped work)
- commit not on the target: refused naming it, zero events (prevents: claiming delivery that did not land)
- only `--delivered-by` or only `--landed-on`: exit 2, zero events (prevents: half a proof)

## Reference coverage
2 reference test function(s): `test_close_delivered_by_records_the_proof_and_closes_as_completed`, `test_close_delivered_by_refuses_unlanded_work_and_half_a_proof`

## Qew today
Missing. A closed item never unblocks dependents (readiness requires `completed`).
