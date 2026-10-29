id: 042cxmtkz
kind: issue
title: Managed-label filter on every view
parent: 042cxmth3
needs: 042cxmtky
labels: area:project-parity area:board
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: rsrmurwp
---
When the target mirror is an overlay (select narrows items), every view filter is prefixed with the managed-label filter (`label:qew:managed`) so human issues stay out; repository mode (select empty) leaves filters bare. Items synced carry the `qew:managed` label.
Scenarios (named walks, each stating the failure it prevents):
- golden: overlay mirror prefixes all eight filters
- golden: repository mode leaves filters bare
- prevents human-owned issues appearing on qew's board
