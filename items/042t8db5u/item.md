id: 042t8db5u
kind: issue
title: qew export reports a false parent cycle when an epic needs its own child
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-16T07:38:36Z
---
set EPIC --needs CHILD is legal, but export --json orders items by parent and need edges together, finds no free item and says parent edges form a cycle. Import creates all items before applying edges, so order need not break such a loop; a real parent cycle must still be refused. Santa asked.
