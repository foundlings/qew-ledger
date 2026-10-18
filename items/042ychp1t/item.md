id: 042ychp1t
kind: issue
title: Commit baselines for items whose sync state is only local on upgrade
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-18T20:35:44Z
discovered_from: 042ybwsg8
evidence: soqssywvvpuu nvkowrllzntp
---
6.31.0 commits a baseline only when an item's sync state changes, so a machine upgraded with existing local .qew/state never commits baselines for unchanged items and a clone still starts without them. At the start of a sync, write a committed baseline for every mirrored item that has legacy local state and no committed baseline.
