id: 044ystebs
kind: issue
title: Lazy snapshot, then evidence and start read only their items
parent: 044ysrkf3
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T19:29:04Z
---
## Problem

evidence and start call the full snapshot although they read one item, its ancestors and its needs.

## Done when

Ledger.snapshot(lazy=True) exists, evidence retract repair and start use it, their trace shows ledger snapshot (lazy) and no full snapshot, output equals the full snapshot's, QEW_NO_LAZY=1 restores the full one
