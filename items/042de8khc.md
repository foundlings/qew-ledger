id: 042de8khc
kind: issue
title: qew restore --to TARGET recreates forge state from the ledger alone
parent: 
needs: 
labels: area:replication replication
owner: 
priority: 2
created: 2026-10-08T22:59:35Z
---
<!-- qew-duplicate -->

Contract: Replication 5.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: empty forge fake rebuilt with issues, links, board
- golden: idempotent second run changes nothing
- adversary: forge down halfway resumes without duplicates (marker adoption)

---
042cxmtny · approved · issue
Parent: #239
Blocked by: #247
