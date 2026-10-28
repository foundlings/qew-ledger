id: 042cz0yg3
kind: issue
title: qew forge migrate --to TARGET
parent: 042cz0y86
needs: 042cz0yg0 042cz0ye1
labels: area:authority
owner: 
priority: 2
created: 2026-10-08T17:48:53Z
evidence: lzuputsr
---
Contract: docs/specs/ledger.md, Authority and topology.
Restore the ledger onto the target, verify counts, switch primary, demote old primary to read-only (or --remove-old). Idempotent, resumable.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: migrate between two fake forges ends with primary switched and old read-only
- adversary: crash midway resumes without duplicates
- refusal: verification mismatch leaves primary unchanged
