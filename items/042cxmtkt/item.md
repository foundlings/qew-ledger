id: 042cxmtkt
kind: issue
title: qew pr merge refuses when a linked item has open child tasks
parent: 042cxmtks
needs: 
labels: area:merge-gate
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
Linked items = the PR's recorded item. Refuse listing the open children.
Scenarios:
- refusal: open task blocks merge; prevents merging half-done work
- golden: all tasks complete allows merge
