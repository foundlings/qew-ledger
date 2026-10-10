id: 042fjjjg1
kind: issue
title: An offline claim whose rival's event id sorts earlier is skipped by sync instead of recorded as lost
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T00:37:14Z
---
Found 2026-10-10 as the ~18 percent flake of test_offline_claim_walk (ledger-remote walk): ids minted in the same second order at random across machines, so a rival's pushed claim can sort before the provisional one. The fold then already marks the provisional claim contested, claim_reconcile.provisional_claims only listed claims that hold the item, so sync reported 'no mirror targets configured' with exit 0 and never wrote claim_lost. Fix (done on branch claim-order): provisional_claims also lists provisional claims the fold marks contested, so they settle as lost (exit 3). Deterministic walk added; the old flaky walk passes 40 of 40. Draft: needs the owner's approval to merge.
