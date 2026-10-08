id: 042cxmtm1
kind: issue
title: Item Status and Priority projection kept in sync
parent: 042cxmth3
needs: 042cxmtky
labels: area:project-parity board
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
After sync every board item has Status from the status model and Priority P0-P4 from the item priority (0-4; larger values clamp to P4 with a warning); changes are verified by reading back with bounded retry; drift is repaired on the next sync; items leaving the target's select are pruned from the board only.
Scenarios (named walks, each stating the failure it prevents):
- golden: claim moves the card to In progress, completing moves it to Done
- golden: priority change updates the Priority field
- adversary: eventual-consistency lag on the forge is retried within bounds then reported, never recorded as synced
- refusal: prune never closes an issue
