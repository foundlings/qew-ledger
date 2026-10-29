id: 042cxmtiy
kind: issue
title: qew export writes items as Markdown files with fixed headers
parent: 042cxmtix
needs: 
labels: area:export-import
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: osnuookw
---
`qew export DIR` writes items/<ID>.md-compatible files and an events summary, deterministic.
Scenarios:
- golden: export then import into an empty ledger reproduces items
- adversary: ids that would escape the directory are refused
