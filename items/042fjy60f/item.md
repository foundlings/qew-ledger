id: 042fjy60f
kind: issue
title: A slow jj push or fetch must not fail a finished command: proportionate timeout, and a timeout is offline, not exit 3
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T00:45:11Z
---
Santa 2026-10-10 (foundlings, 20874 items): qew sync exited 3 with 'jj --no-pager git timed out after 5.0s' although the work completed (unpushed 0, pending 0). Causes: the 5s [replication] timeout_s also bounds jj commands, which snapshot a ~60k-file working copy first; and a timeout raised QewError exit 3 from push and fetch, which are best effort everywhere else. Fix: jj commands get at least 60s (QEW_JJ_TIMEOUT_S overrides); a timeout of a fetch or push is treated like an unreachable remote (remembered as the failure, outcome offline, the commit stays local and the next write or qew sync pushes it), never exit 3 for a command whose own work finished.
