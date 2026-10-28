id: 042cz0ydz
kind: issue
title: [authority] primary configuration and status
parent: 042cz0y86
needs: 
labels: area:authority
owner: 
priority: 0
created: 2026-10-08T17:48:53Z
evidence: xvrrtysx
---
Contract: docs/specs/ledger.md, Authority and topology.
Parse `[authority] primary = target slug | "none"` (default none); unknown targets fail; shown by `qew status`.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: default none, named target accepted
- refusal: unknown target or wrong type fails with the file named
