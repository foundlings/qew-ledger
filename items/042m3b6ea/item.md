id: 042m3b6ea
kind: task
title: Restore qew-ledger automatic pushes blocked by an undescribed jj ancestor
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-12T18:33:11Z
---
Behavior: qew writes push the ledger to origin automatically. Adversary: an empty ancestor without a description causes jj to reject every later push. Repair the existing ancestor description without squashing history; sync and verify zero unpushed changes.
