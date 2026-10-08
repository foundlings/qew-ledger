id: 042cxmth9
kind: issue
title: Board grouping: column, owner, label, epic, parent
parent: 042cxmth2
needs: 042cxmth6
labels: area:board
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
`--group-by column|owner|label|epic|parent` renders sections instead of or inside columns.
Scenarios:
- golden: group by epic lists each epic's children; prevents orphan cards
- golden: multi-label items appear under each label; prevents hiding overlap
- refusal: unknown group key exits 2
