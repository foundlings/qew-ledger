id: 043f66nch
kind: issue
title: Ledger lock is unfair and fixed at 60s, so a busy machine can starve an agent
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-27T04:54:42Z
evidence: e929757ca30a50d3dc52c8cd1b6c104e0cba5fec 83a32dca084827ae49dc6f98ff20496bda21041c
---
## Goal

Waiters poll flock with jitter, so whichever process polls at the right instant wins and an unlucky agent (Rudolph's qew pr merge behind elf3) times out again and again with 'locked by ... waited 60s'. The 60s is fixed (LOCK_WAIT_SECONDS) and waiter markers are read only by the background sync. Serve waiters roughly in arrival order so none starves, make the wait settable (config replication lock_wait_s, env QEW_LOCK_WAIT_S), and have the timeout message name the queue. Never a deadlock: the queue is a bounded courtesy over the kernel lock; a dead, stopped or stale waiter, or a deferral past a cap, is ignored, and the kernel flock stays the only mutual exclusion.

## Done when

A walk shows three waiters take the lock in arrival order with no starvation; a dead waiter marker and a stopped (stale) waiter never block the others; a deferral never outlasts its cap; lock_wait_s and QEW_LOCK_WAIT_S change the wait; the timeout text names the queue; specs and README agree; full gate green.
