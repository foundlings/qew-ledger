id: 042cxmtny
kind: issue
title: qew restore --to TARGET recreates forge state from the ledger alone
parent: 042cxmtnm
needs: 042cxmtnr
labels: area:replication replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: Replication 5.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: empty forge fake rebuilt with issues, links, board
- golden: idempotent second run changes nothing
- adversary: forge down halfway resumes without duplicates (marker adoption)
