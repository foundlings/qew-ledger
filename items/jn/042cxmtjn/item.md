id: 042cxmtjn
kind: issue
title: Add `qew --version` printing the package version offline
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: xonquotz
---
## Behaviour
`qew --version` prints `qew X.Y.Z` (the installed package version), exits 0, touches no ledger, no network and no forge, and works outside any repository.

## Scenarios
- Outside a repo: stdout matches `^qew \d+\.\d+\.\d+\n$`, no subprocess or HTTP call recorded. Prevents users being unable to identify the installed build or the command needing credentials.
- Version equals the package metadata and the release tag check in the release issue.

## Reference coverage
1 test (version flag).

## Qew today
Missing: no `--version` option in `cli.py`, no test.
