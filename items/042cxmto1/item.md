id: 042cxmto1
kind: issue
title: Detached background sync after every write (token-free)
parent: 042cxmtnm
needs: 042cxmtnn 042cxmtnr 042cxmtnq
labels: area:replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
evidence: tmuqzlvtpqmz
---
Contract: docs/specs/ledger.md Replication, Background sync. After a write qew spawns one detached worker (ledger push + all mirror targets) with a lock, a timeout and a log in `.qew/`; foreground prints at most `sync: queued`.
Scenarios (each a named walk stating the failure it prevents):
- golden: a write returns before the worker finishes (forge fake with a delayed response); prevents agents waiting on forges
- adversary: concurrent writes start one worker only (lock); prevents double sync and duplicate issues
- adversary: a failing forge leaves pending state and the next command's worker clears it
- adversary: stale lock from a killed worker is detected by pid and cleared
- golden: QEW_OFFLINE=1 and background_sync=false spawn nothing
- golden: foreground output is at most one line and never contains forge text
- golden: sync.log is bounded and visible via qew status
