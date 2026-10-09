id: 042fcpx9w
kind: issue
title: Learned pace must not mislearn: ignore thin evidence, expire stale budgets, show it in status
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T22:17:27Z
---
Owner 2026-10-09 (on 3.4.0): the learned pace may learn badly when GitHub changes its rates. Fixes: a block preceded by fewer than 20 recorded creates in the window teaches nothing (it was probably caused by something else, e.g. another machine); a learned budget expires 6 hours after it was last set or raised, returning to the documented default; the budget moves both ways (a later block with more creates replaces a lower one); qew status shows the learned pace so a person can see and reset it (delete the target's pace.json). Walks for each.
