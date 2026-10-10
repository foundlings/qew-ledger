id: 042d1mvdv
kind: issue
title: qew pr: adopt an existing pull request for a head, and close one (orphans after a crash between forge accept and mirror write)
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-08T18:41:55Z
---
Draft. PRs #288 and #289 were opened by an earlier qew pr open whose assignee step failed, so no mirror records them; re-opening from the same head fails. Needs a marker-based find_pull_request for open, and a qew pr close command.
