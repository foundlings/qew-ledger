id: 042za6752
kind: issue
title: qew land completes only the items in the pull request record, not the ones its Progress boxes name
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-19T07:42:47Z
---
A member pull request merged through a batch pull request: qew land --integrator completed only the first covered item and left 14 items claimed with evidence on main. land walks the record's items, which freeze at open, and a pull request's later Progress boxes never reached the record; a merged pull request cannot have its covered items synced afterwards. land must also cover every item the merged body's Progress boxes name: complete those whose evidence is the merged head or an ancestor of it, and report the others naming what to do.
