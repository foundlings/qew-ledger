id: 042cxmth6
kind: issue
title: qew board renders the kanban in the terminal
parent: 042cxmth2
needs: 042cxmth5
labels: area:board
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
Columns the seven statuses Draft / Backlog / Ready / Needs approval / In progress / In review / Done, cards with id, title, owner, priority, labels; width-aware text layout, no color codes when not a TTY.
Scenarios:
- golden: five columns with cards; prevents unreadable output
- adversary: titles with control characters or bidi marks are shown escaped; prevents terminal injection
- golden: empty ledger renders empty columns with counts
