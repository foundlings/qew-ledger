id: 042cxmth5
kind: issue
title: Derive board state from ledger events and a per-board config file
parent: 042cxmth2
needs: 042cxmth4
labels: area:board
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
Behaviour: status derived exactly as in the status-model issue (project-parity); board config lives in `boards/<name>.json` style ledger files (one file per board: columns, default sort/group/filter), no forge needed.
Scenarios:
- golden: item moves Draft->Ready->In progress->In review->Done as events are written; prevents the board disagreeing with readiness
- refusal: a board file with unknown columns or duplicate names fails `qew check`; prevents silent mis-rendering
- adversary: a forge outage leaves the board unchanged; prevents board reads needing network
