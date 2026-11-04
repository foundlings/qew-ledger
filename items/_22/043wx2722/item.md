id: 043wx2722
kind: issue
title: Publish the sync worker startup marker before spawning it
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-04T12:16:17Z
discovered_from: 043wwfc18
evidence: plyrulll oxunyuks
---
## Problem

A worker can acquire its lock and exit before Popen returns. The parent then writes sync.starting after the worker cleared it, so the next queued write sees a nonexistent worker and remains unsynced. Deterministic reproduction: two queue calls spawn once, worker_running stays true after exit, and the second id stays queued. Observed full gate synced five of six burst items.

## Fix

Write the startup marker before spawning, clear it if spawning fails, and preserve spawn errors. Add deterministic fast-worker and failed-spawn regression walks.

## Done when

The fast worker cannot leave a stale startup marker, failed spawn leaves no marker, concurrent burst walks and the full release gate pass.
