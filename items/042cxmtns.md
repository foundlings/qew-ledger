id: 042cxmtns
kind: issue
title: Pending state derived from event ids and mirror synced_event
parent: 042cxmtnm
needs: 
labels: area:replication replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: Replication 3. Pure function used by sync, status and auto push.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: matrix of (no mirror, behind, current, selected-out)
- adversary: mirror file edited by hand to a future event id is reported by check
