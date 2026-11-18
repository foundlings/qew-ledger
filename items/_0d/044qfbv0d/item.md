id: 044qfbv0d
kind: issue
title: qew evidence --repair: replace git-hash-only evidence on a completed item
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-18T15:57:45Z
discovered_from: 044qdr89f
evidence: mkormmmq
---
## Problem

Completed items 044b5zzg9, 044grx5bt, 044hjd13z carry only git-hash evidence and qew evidence refuses completed items, so it cannot be repaired short of reopening. Add --repair (or document reopen) and make qew check name such items with the exact command.

## Done when

qew evidence ID --change X --repair works on a completed item, recorded as an event; qew check names git-hash-only completed items with the command
