id: 042cxmto5
kind: issue
title: Commit message references to ledger IDs
parent: 042cxmto2
needs: 042cxmto3
labels: area:vcs-hook
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: prylwoyt
---
Mechanical parser for `Refs: ID` trailers; unknown ids reported.
Scenarios:
- golden: trailer parsed
- adversary: lookalike ids ignored
