id: 042f0m67k
kind: issue
title: Forge writes run in parallel: a bounded worker pool for sync, restore and migrate with shared rate-limit backoff
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T18:10:16Z
---
Owner 2026-10-09 via Santa: file and update many issues, PRs and cards in parallel instead of sequentially (stdlib concurrent.futures, [replication] forge_concurrency with a sane default). Keep: per-item ordering (create before update/close/card; mirror written after the create is accepted), duplicate guard and lowest-number-wins, resumability after a kill, one ledger commit per batch, a 403/429 with retry-after pauses every worker and is reported. Walks: N items in parallel give the same ledger and forge state as sequential; a mid-run kill resumes without duplicates; a rate-limit response pauses all workers. Order: after the close-reason bug 042f0gp5t and the per-create cost 042f0ip9w.
