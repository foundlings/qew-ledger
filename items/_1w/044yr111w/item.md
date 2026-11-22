id: 044yr111w
kind: issue
title: A write verb resolves an exact item id without listing the ledger
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T18:52:41Z
evidence: pquntrzz ttutpwlo yxztkrww nmvrlvsn
---
## Problem

qew comment (and the other write verbs that resolve an item) list all 27,836 item directories and scan every item header for aliases while holding the ledger lock: about 3 s of an 8 s write on foundlings.

## Approach

An exact id that has an item file goes straight to it; a sidecar records that the ledger has no aliases at all, so the alias scan is skipped, and any write of an item file or any merged fetch removes it.

## Done when

qew comment on a 28k-item ledger no longer lists the items, a ledger with aliases still resolves old ids, and the walks cover both
