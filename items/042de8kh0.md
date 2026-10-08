id: 042de8kh0
kind: issue
title: Local per-checkout write lock
parent: 
needs: 
labels: area:replication
owner: 
priority: 2
created: 2026-10-08T22:59:35Z
---
<!-- qew-duplicate -->

Contract: Replication 8. Advisory flock on `.qew.lock` (VCS-ignored) held for the write+commit; reads never lock.
Scenarios (each a named walk whose docstring states the failure it prevents):
- adversary: two processes creating items concurrently both succeed with distinct ids and two commits; prevents interleaved commits and id collisions
- refusal: lock held longer than timeout exits 3 naming the holder pid

---
042cxmtno · approved · issue
Parent: #239
