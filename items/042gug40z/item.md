id: 042gug40z
kind: issue
title: Open a PR for a ledger-only task without requiring an issue mirror
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T15:53:59Z
---
In foundlings, mirror select=kind:epic,issue intentionally leaves tasks ledger-only. qew pr open 042gbvhf8 refuses with zero matching issue mirrors; qew sync --item creates nothing because the selector excludes tasks. Support PR hosting through the task tracking issue or an explicit repository target while preserving task evidence and covered-item state. Reproduce with a task under a mirrored issue, no task mirror, and an explicit pushed branch. Done when qew pr open can open that PR without changing mirror selection or task kind.
