id: 044rjrpcg
kind: issue
title: Op-log collection holds the ledger write lock for minutes: collect detached, in short bounded steps
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-11-19T05:22:39Z
---
## Problem

A write's op_gc.maybe_collect takes the ledger write lock and runs jj op abandon ..<op> plus jj util gc inside it (up to 900s per jj call). On the Foundlings ledger one evidence command held the lock 11+ minutes with ~10 writers (agents, elves, integrator qew land) queued behind it. Reported by Santa 2026-11-19.

## Done when

A write never waits for or runs op-log collection: it starts a detached collector (own gc.lock, one at a time). The collector abandons old operations in bounded batches, taking the write lock only per batch (never waiting more than moments, skipping when busy) so lock hold time stays small whatever the log size. qew gc --now runs a collection in the foreground on demand. The 'locked by' message names holder, verb and age and, for a collector, says qew gc status/--now. Reads never wait for the write lock (verified). Walk tests prove each.
