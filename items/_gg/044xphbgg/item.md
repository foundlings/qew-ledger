id: 044xphbgg
kind: issue
title: A ledger write holds the lock minutes: full-tree jj snapshot per commit, stale lock.waiting files
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T06:26:46Z
discovered_from: 044xjcigz
---
## Where

src/qew/ledger_repo.py (jj commit), filelock.py (waiter markers), replication write session

## Problem

On the 27k-item foundlings ledger each write holds the lock about 2.5 minutes, mostly jj commit (full working-copy snapshot, 1m33s seen). About 15 agents drain one write per 2-3 minutes. About 50 stale .qew/lock.waiting.* files date back days; unknown whether the snapshot scans them (they may need to be ignored or never created inside the tree). Each try waits a fixed 60s and ignores QEW_REPO_LOCK_WAIT_S in some verbs (related: 044xjcigz).

## Fix

Measure where commit time goes; keep waiter markers out of the snapshot (ignored path or outside the tree) and reap dead ones; commit only the touched paths (jj commit <paths>) or batch queued writes; honor the lock-wait env var everywhere.

## Done when

A walk with many ledger files shows a write snapshots only its paths, stale waiter markers are reaped, and the env var is honored in every verb.
