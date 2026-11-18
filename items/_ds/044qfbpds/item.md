id: 044qfbpds
kind: issue
title: qew check: items/ID and events/ID reported as belonging to no item although the item exists in its shard
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-18T15:57:39Z
discovered_from: 044qdr89f
---
## Problem

Foundlings audit: qew check reports events/044qev99r and items/044qev99r belong to no item, graph orphans=2, yet items/_9r/044qev99r exists with parent 042oidxb2.

## Done when

a walk reproduces it (or finds the true cause) and qew check is clean for a correctly sharded item
