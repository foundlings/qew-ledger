id: 042cxmtkx
kind: issue
title: qew land completes items whose PR merged
parent: 042cxmtks
needs: 042cxmtku
labels: area:merge-gate
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
After `qew pr merge`, `qew land PR` records evidence of the merge head and completes the claimed item if gates pass.
Scenarios:
- golden: merge then land completes
- refusal: land of an unmerged PR refused
