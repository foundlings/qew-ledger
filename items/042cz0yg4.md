id: 042cz0yg4
kind: issue
title: qew ledger fork --to REMOTE [--primary TARGET]
parent: 042cz0y86
needs: 042cz0ydz
labels: area:authority
owner: 
priority: 2
created: 2026-10-08T17:48:53Z
---
Contract: docs/specs/ledger.md, Authority and topology.
New ledger identity with lineage; items and events kept; mirrors, boards, claims, divergences dropped; re-merge into origin refused.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: forked ledger has the same items, no mirrors or owners, forked_from set
- refusal: merging the fork back into the origin is refused
- golden: fork with --primary points at a fresh target
