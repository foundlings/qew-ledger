id: 042cxmtjm
kind: issue
title: Keep the post-push evidence reminder bounded and owner-scoped
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: rqvnrumn
---
## Behaviour
Qew-specific (no reference counterpart): one line after `git push` or `jj git push` for claimed items of the current actor lacking evidence; nothing otherwise.

## Scenarios
Covered: reminder with a claim lacking evidence; silent without claims or outside a repo; another actor's claim ignored.

## Reference coverage
None (qew-only). Listed so the audit accounts for the three qew post-tool walks.

## Qew today
Covered.
