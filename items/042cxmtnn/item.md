id: 042cxmtnn
kind: issue
title: Every qew write commits itself to the ledger repo (jj or git)
parent: 042cxmtnm
needs: 
labels: area:replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Contract: docs/specs/ledger.md Replication 1. Commit exactly the paths a command wrote, message `qew: <verb> <ID> [by <actor>]`; detect jj (colocated) vs git; atomic with rollback.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: create/set/start/evidence/complete each leave one commit with the structured message and a clean tree; prevents forgotten commits
- refusal: the commit fails (hook, locked index) and the files this command wrote are removed or restored; prevents uncommitted-write state
- adversary: crash between write and commit; next command reports `uncommitted` and commits `qew: recover`
- golden: batch `create --from-file` makes one commit for N items
- golden: a ledger with unrelated dirty files commits only qew's paths
