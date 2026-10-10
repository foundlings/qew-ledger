id: 042cxmth8
kind: issue
title: Board sorting: priority, updated, created, title
parent: 042cxmth2
needs: 042cxmth6
labels: area:board
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
`--sort priority|updated|created|title[:desc]` like GitHub Projects boards; updated derives from the newest event.
Scenarios:
- golden: each key orders cards as documented
- refusal: unknown sort key exits 2 naming valid keys; prevents silent default ordering
