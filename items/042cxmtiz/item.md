id: 042cxmtiz
kind: issue
title: qew import reads Markdown files with fixed headers
parent: 042cxmtix
needs: 042cxmtiy
labels: area:export-import
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
Mechanical, header-only parse; unknown keys fail; ids kept.
Scenarios:
- golden: import of exported tree
- refusal: duplicate ids refused before any write; malformed header names the file
