id: 042cz0yfz
kind: issue
title: Working on items you do not hold is refused
parent: 042cz0y86
needs: 042cz0ye0
labels: area:authority authority
owner: 
priority: 1
created: 2026-10-08T17:48:53Z
---
Contract: docs/specs/ledger.md, Authority and topology.
evidence, comment-progress and complete require holding the item or an ancestor; completing offline is allowed with evidence.
Scenarios (each a named walk whose docstring states the failure it prevents):
- refusal: evidence on someone else's claimed item
- golden: epic holder completes a descendant offline
- adversary: a stale claim_lost owner cannot complete
