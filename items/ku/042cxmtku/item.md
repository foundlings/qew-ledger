id: 042cxmtku
kind: issue
title: qew pr merge refuses without recorded evidence for the linked item
parent: 042cxmtks
needs: 042cxmtkt
labels: area:merge-gate
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
The checked head must be covered by an evidence event of the item before merge.
Scenarios:
- refusal: no evidence blocks merge
- golden: evidence recorded then merge passes
