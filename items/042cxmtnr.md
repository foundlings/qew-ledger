id: 042cxmtnr
kind: issue
title: Opportunistic push of affected items to every mirror target after a write
parent: 042cxmtnm
needs: 042cxmtnn 042cxmtnp
labels: area:replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: Replication 3. Time budget, per-target isolation, pending derived from event ids (no outbox files).
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: claim in the ledger updates the issue and board column on all targets without running sync
- adversary: forge A down mid-sync: B still updated, write succeeds, pending shown for A, later command catches up
- golden: an item with no mirror file is pending and gets created
- prevents: a second command re-sending already synced items (idempotent)
