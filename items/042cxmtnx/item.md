id: 042cxmtnx
kind: issue
title: qew import --from TARGET (and ad hoc --forge/--repo)
parent: 042cxmtnm
needs: 042cxmtnn 042cxmtnu
labels: area:replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: Replication 4,5. Read issues, PRs, labels, comments (and board column) from a forge project into ledger items with mirrors and provenance forge-import; closed issues import closed or completed(import) with --history.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: empty ledger plus a populated forge fake equals items, parents/dependencies, mirrors and board columns
- golden: re-import is idempotent (adopts by marker or mirror, no duplicates)
- adversary: pagination limit, malformed forge JSON and a forge that lies about numbers fail loudly with nothing partial
- golden: ad hoc --forge gitlab --repo URL without a config target
