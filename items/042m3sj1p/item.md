id: 042m3sj1p
kind: issue
title: Prevent empty undescribed jj ledger checkpoints from blocking automatic pushes
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-12T18:42:44Z
---
Regression: a normal qew write must push past an empty undescribed ancestor without rewriting change IDs or permitting undescribed content commits. Exercise a real jj ledger and local bare remote, commit the failing command walk first, then implement narrowly scoped handling and run the full gate.
