id: 042cxmtkw
kind: issue
title: qew complete can never bypass a gate
parent: 042cxmtks
needs: 
labels: area:merge-gate
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
No flag, env var, event hand-edit or provenance value lets `complete` skip claim, children or evidence; hand-edited events fail `qew check`.
Scenarios:
- adversary: completed event written by hand without evidence fails check
- adversary: provenance import written outside --import is refused at check
- refusal: complete on a draft, unclaimed, blocked or closed item
