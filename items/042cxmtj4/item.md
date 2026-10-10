id: 042cxmtj4
kind: issue
title: qew ready orders by priority then dependency depth
parent: 042cxmtj1
needs: 
labels: area:graph-ready
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
Within a priority, items that unblock the most dependents (or deepest chain) come first; ties by id.
Scenarios:
- golden: deterministic order
- prevents starvation of items that unblock others
