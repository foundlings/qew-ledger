id: 042cxmtm2
kind: issue
title: Fix org project #1 (qew board) to match the full board
parent: 042cxmth3
needs: 042cxmtky 042cxmtm1
labels: area:project-parity board
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
Run the new `project ensure` against foundlings/qew board #1, verify through the GitHub API that Status options, Priority field and eight views match, re-place all items.
Scenarios (named walks, each stating the failure it prevents):
- golden: live check output recorded as a comment on this issue
