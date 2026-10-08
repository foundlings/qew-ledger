id: 042cxmtnu
kind: issue
title: Incremental pull: forge-side content edits become events
parent: 042cxmtnm
needs: 042cxmtnn 042cxmtns
labels: area:replication replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: Replication 4. Title/body/label edits and new comments made outside qew become `field`/`commented` events with provenance `forge`; then pushed to the other targets.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: label added on target A appears in the ledger and on target B
- adversary: hostile title/comment text is stored as data, rendered escaped, never executed or used as a path
- golden: re-pull with no changes writes nothing (idempotent)
- adversary: forge down mid-pull records nothing partial
