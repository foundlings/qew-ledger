id: 042cxmtj2
kind: issue
title: qew graph --format text|dot|mermaid
parent: 042cxmtj1
needs: 
labels: area:graph-ready
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: omslnoop
---
Dependency edges and parent edges as text, Graphviz dot and Mermaid; deterministic order.
Scenarios:
- golden: each format for a diamond graph
- adversary: titles with quotes and newlines are escaped in dot and mermaid
