id: 042cxmtnp
kind: issue
title: [replication] config and QEW_OFFLINE
parent: 042cxmtnm
needs: 
labels: area:replication replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: Replication 7. auto_commit/auto_push/auto_forge_sync/timeout_s with defaults; QEW_OFFLINE=1.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: defaults on; each switch off disables exactly its step
- refusal: unknown key or wrong type fails with the file named
- golden: QEW_OFFLINE=1 makes zero network calls (fake forge and remote record none) yet still commits locally
