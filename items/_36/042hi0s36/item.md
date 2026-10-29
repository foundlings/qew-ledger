id: 042hi0s36
kind: issue
title: Support owner-authorized disposition of unmarked legacy pull requests
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T23:55:02Z
evidence: vunqxrxuvkvp mrupzutqprql
---
## Where

qew pr open and qew pr close; reproduced against foundlings/foundlings PR #2424.

## Goal

Allow an explicitly assigned owner to adopt and close an existing unmarked legacy PR through qew without a forge bypass.

## Approach

Preserve the default refusal to take over an unmarked stranger PR. Add an explicit auditable owner-authorized adoption or disposition path that links the existing PR to its ledger item without creating a duplicate PR.

## Done when

Red controls prove unmarked stranger PRs remain protected, explicit authorized legacy adoption preserves the existing PR number and head, and qew pr close can then close only that recorded PR. Reproduction: qew pr close 2424 refuses because it is not recorded; qew pr open ADF --head adf-identity-keys --base main refuses because the existing PR has no qew marker and requests a forge-side close. The project prohibits that bypass.
