id: 042ydp931
kind: issue
title: Cache the committed baselines in snapshot.db, refreshed incrementally when a pull changes them
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-18T20:59:59Z
---
Baselines are one small file per item and target; reading thousands of them on every status and sync is the slow path the snapshot cache exists for. Keep the newest baseline of each (item, target) in .qew/snapshot.db beside a stat signature of its directory, and re-read only the directories whose stat changed, so baselines pulled in from another machine are picked up without a full re-read.
