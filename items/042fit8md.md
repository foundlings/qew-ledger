id: 042fit8md
kind: issue
title: Epic letter ids are the default id_mode: epic letters, issue and task base35-time
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T00:21:53Z
---
Owner 2026-10-10: 'can we make the phase letter mode for epics the new default?'. A ledger without id_mode gets epic = letters, issue and task = base35-time; qew init writes the table explicitly. Explicit settings (qew's own ledger, foundlings) are unchanged. Letters are not merge-safe for concurrent epic creation on two machines (a loud git conflict, not silent): epics are rare and human-made.
