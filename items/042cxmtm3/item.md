id: 042cxmtm3
kind: issue
title: Boards on GitLab (scoped label board) and Forgejo (labels)
parent: 042cxmth3
needs: 042cxmth4
labels: area:project-parity area:board
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: oswllzqk
---
GitLab: board with lists for each Status as scoped labels `board::<Status>` and priority labels; Forgejo: unsupported board, state labels carry the same statuses.
Scenarios (named walks, each stating the failure it prevents):
- golden: GitLab fake board lists match the seven statuses
- refusal: Forgejo ensure is unsupported and says so
