id: 042cxmtk3
kind: issue
title: Add `qew complete --take-over` that records the previous holder
parent: 042cxmtjw
needs: 042cxmtk0 042cxmtk1 042cxmtk2
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lyrtzqmu
---
## Behaviour
`qew complete ITEM --take-over --reason TEXT` proves the completion evidence first, then completes work another actor holds, recording `taken_over_from` and the completer on the `completed` event (the reference appends `Taken over from LOGIN by CALLER` to the closing comment). Refused before any write when no other actor holds the item (2) or evidence fails. It also clears a claim left behind when a forge closed the mirrored issue first (see `stale-claims-report`).

## Scenarios
- golden: A holds, B completes with take-over; evidence proven, one `completed` event naming A and B (prevents: losing whose claim was finished)
- plain complete on A's claim: exit 3 naming `--take-over` (prevents: silent takeover; covered by complete-ownership)
- take-over when the caller already holds it or nobody holds it: exit 2 `nothing to take over`, no event
- evidence not on the target branch: refused, claim not cleared (prevents: freeing a claim for unproven work)

## Reference coverage
4 reference test function(s): `test_complete_still_refuses_another_logins_claim_without_take_over`, `test_complete_take_over_closes_open_work_and_records_the_previous_holder`, `test_complete_take_over_clears_a_stale_claim_on_work_github_already_closed`, `test_complete_take_over_without_another_logins_claim_is_refused`

## Qew today
Missing.
