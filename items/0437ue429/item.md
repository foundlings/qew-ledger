id: 0437ue429
kind: issue
title: qew land --integrator refuses 'nothing to take over' when the caller already holds the item (directly or through its epic)
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-23T13:31:59Z
evidence: xxtmusnxslpz ltulltuutmyn
---
## Problem

land treats an item as another actor's claim whenever the recorded owner is not the caller, so an integrator who holds the item's epic (or whose claim was re-read) gets 'nothing to take over: you already hold' and nothing is recorded; reported by foundlings for qew land 4992.

## Done when

land skips the takeover when the caller already holds the item, records the merged head as evidence and completes it
