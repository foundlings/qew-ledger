id: 042cz0yg1
kind: issue
title: Item headers carry ledger-level links only (tracks, pr)
parent: 042cz0y86
needs: 
labels: area:authority
owner: 
priority: 2
created: 2026-10-08T17:48:53Z
---
Contract: docs/specs/ledger.md, Authority and topology.
Schema gains `tracks:` and `pr:` (ledger ids); forge numbers and URLs never appear in item files; `qew show` resolves links to forge URLs from mirrors/.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: show prints the issue URL from the mirror index
- refusal: a header containing a URL or number fails check
- golden: adding a forge target rewrites no item file
