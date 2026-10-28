id: 042cz0yg2
kind: issue
title: Code and ledger repos pushed to every forge target
parent: 042cz0y86
needs: 042cz0ydz
labels: area:authority
owner: 
priority: 2
created: 2026-10-08T17:48:53Z
evidence: zukwvupp
---
Contract: docs/specs/ledger.md, Authority and topology.
Per target git remote `qew-<slug>` for both repos, pushed by sync; creating the forge repo is out of scope (must exist).
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: both repos reach a bare remote per target
- adversary: one unreachable target does not block the others
- refusal: missing remote URL is reported not guessed
