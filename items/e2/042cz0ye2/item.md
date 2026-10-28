id: 042cz0ye2
kind: issue
title: Claim arbitration through the ledger remote when primary is none
parent: 042cz0y86
needs: 042cz0ye0
labels: area:authority
owner: 
priority: 0
created: 2026-10-08T17:48:53Z
evidence: uwuluxru
---
Contract: docs/specs/ledger.md, Authority and topology.
claimed, push, claim_confirmed on success; rejected push fetches and writes claim_lost when another claim exists; no remote = single writer confirms at once; unreachable configured remote refuses start.
Scenarios (each a named walk whose docstring states the failure it prevents):
- adversary: two clones race a claim: exactly one confirmed, the other claim_lost
- golden: single-writer ledger without remote confirms immediately
- refusal: remote configured but unreachable refuses start
