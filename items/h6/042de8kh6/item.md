id: 042de8kh6
kind: issue
title: Forge-side state changes become forge_divergence events
parent: 
needs: 
labels: area:replication
owner: 
priority: 2
created: 2026-10-08T22:59:35Z
---
<!-- qew-duplicate -->

Contract: Replication 4. Closed/reopened/assignee/board column changes on the forge never override ledger state.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: issue closed on GitHub creates one divergence, ledger state unchanged, shown by status
- adversary: a forge-side PR merge around qew creates a divergence and never completes the item
- golden: the same divergence is not duplicated on the next pull

---
042cxmtnv · approved · issue
Parent: #239
Blocked by: #250
