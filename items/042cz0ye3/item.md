id: 042cz0ye3
kind: issue
title: Claiming an epic claims its open descendants atomically
parent: 042cz0y86
needs: 042cz0ye1 042cz0ye2
labels: area:authority
owner: 
priority: 1
created: 2026-10-08T17:48:53Z
evidence: uwuzoqtp
---
Contract: docs/specs/ledger.md, Authority and topology.
All-or-nothing with rollback; descendants already claimed by others refuse the whole operation.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: epic claim claims issues and tasks
- refusal: one descendant held by another refuses everything and writes nothing
- golden: releasing the epic releases the cascade
