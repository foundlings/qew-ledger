id: 042cxmtjz
kind: issue
title: Require a reason and an owner check on `qew release`
parent: 042cxmtjw
needs: 042cxmtjy
labels: area:lifecycle
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: opppyqtx
---
## Behaviour
`qew release ITEM --reason TEXT [--force]` frees a claim without closing the work. The `released` event records the reason, the releasing actor and the previous owner. Releasing a claim held by another actor is refused (exit 3) unless `--force`; a forced release is marked as forced in the event. Releasing an item that is not claimed is refused (exit 2) with nothing written. `--reason` is mandatory so a recovered claim leaves an audit trail. Lane rules live in `lane-claim-guard`.

## Scenarios
- golden: owner releases with a reason; item returns to approved and appears in `qew ready`; event carries reason and previous owner (prevents: anonymous recovery of work)
- other actor's claim without `--force`: exit 3, nothing written (prevents: accidental release of a sibling's work)
- forced release by another actor: succeeds, event marked forced (prevents: unrecorded takeover)
- release of unclaimed work: exit 2, nothing written (prevents: phantom released events)
- missing `--reason`: usage error exit 2 before any write

## Reference coverage
No dedicated reference test; specified from the reference command documentation. (spec) release command contract; no dedicated reference walk beyond epic and lane tests

## Qew today
Reduced. `qew release ITEM` exists, takes no reason, does not compare the caller with the owner, so any actor can release any claim silently. The flow walk covers only release then ready.
