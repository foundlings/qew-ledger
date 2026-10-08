id: 042cxmtnq
kind: issue
title: Best-effort ledger remote fetch/merge before a write and push after
parent: 042cxmtnm
needs: 042cxmtnn 042cxmtno 042cxmtnp
labels: area:replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: Replication 2. Short timeout; unreachable remote keeps local commits; next command retries.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: two clones; A writes and pushes, B's next command fetches and sees it
- adversary: remote unreachable (bad URL, timeout): write succeeds, commit stays local, `qew status` shows unpushed
- adversary: real text conflict from a hand edit is reported loudly, nothing auto-resolved, writes refuse until fixed
- golden: jj and git ledgers both replicate
