id: 042cxmtnz
kind: issue
title: Multi-agent convergence scenarios (two and three clones)
parent: 042cxmtnm
needs: 042cxmtnq 042cxmtnr 042cxmtnv
labels: area:replication replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Scenario walks with real git/jj clones against a bare remote and a forge fake: A claims and completes, B creates and comments, C works offline then reconnects; all converge to the same items, states and mirrors; includes a forge-side close producing a divergence on every clone.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: three agents converge
- adversary: concurrent creates in the same second yield unique ids
- adversary: offline agent writes, reconnects, merges without conflict
