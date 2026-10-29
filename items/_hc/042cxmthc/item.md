id: 042cxmthc
kind: issue
title: qew board config files: create, list, set default view
parent: 042cxmth2
needs: 042cxmth5
labels: area:board
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: pnpnyqws
---
`qew board create|list|set` manage named board files in the ledger; merge-safe (one file per board).
Scenarios:
- golden: two branches add different boards and merge cleanly
- refusal: duplicate board name refused
