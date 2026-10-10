id: 042cxmtno
kind: issue
title: Local per-checkout write lock
parent: 042cxmtnm
needs: 
labels: area:replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: Replication 8. Advisory flock on `.qew.lock` (VCS-ignored) held for the write+commit; reads never lock.
Scenarios (each a named walk whose docstring states the failure it prevents):
- adversary: two processes creating items concurrently both succeed with distinct ids and two commits; prevents interleaved commits and id collisions
- refusal: lock held longer than timeout exits 3 naming the holder pid
