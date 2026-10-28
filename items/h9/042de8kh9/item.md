id: 042de8kh9
kind: issue
title: qew accept and qew reject resolve a divergence
parent: 
needs: 
labels: area:replication
owner: 
priority: 2
created: 2026-10-08T22:59:35Z
---
<!-- qew-duplicate -->

Contract: Replication 4. accept applies the forge value through the normal gates and writes divergence_accepted; reject keeps ledger state, writes divergence_rejected, next push restores the forge.
Scenarios (each a named walk whose docstring states the failure it prevents):
- refusal: accepting a forge close as completed without evidence is refused by the gate
- refusal: accepting a draft release requires a human quote
- golden: reject restores the forge issue on the next push
- golden: accept of a reopen/close applies and propagates to other targets

---
042cxmtnw · approved · issue
Parent: #239
Blocked by: #251
