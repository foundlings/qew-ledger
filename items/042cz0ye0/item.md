id: 042cz0ye0
kind: issue
title: claim_confirmed and claim_lost events in the fold
parent: 042cz0y86
needs: 042cz0ydz
labels: area:authority
owner: 
priority: 0
created: 2026-10-08T17:48:53Z
evidence: xvrrtysx
---
Contract: docs/specs/ledger.md, Authority and topology.
A `claimed` event named by `claim_lost` is ignored by the fold; `claim_confirmed` is informational; check validates refs.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: lost claim leaves the item approved and unclaimed
- adversary: claim_lost naming a missing event fails check
- golden: two claims with the second lost fold cleanly
