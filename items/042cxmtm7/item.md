id: 042cxmtm7
kind: issue
title: Seed a progress checklist in the PR body from `--body-file` with stable item markers
parent: 042cxmtm4
needs: 042cxmtm6
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
## Behaviour
`qew pr open --body-file FILE` carries a `## Progress` checklist of `- [ ] text <!-- pr-progress:ID -->` lines into the PR body unchanged (still scanned for closing references). Without a body file the PR has no checklist. Markers are the stable address `qew pr check` uses.

## Scenarios
- checklist carried: body file with three marked items -> forge body contains them verbatim and `qew pr check --list` reads three items. Prevents: a checklist that cannot be ticked later.
- file read failure: missing or unreadable body file is exit 2 before any forge call. Prevents: a PR opened with an empty body.

## Reference coverage
Reference command docs (pr body-file progress items); exercised by the checklist walks (see pr-check issues).

## Qew today
Missing: no `--body-file`, no progress markers.
