id: 042cxmtmd
kind: issue
title: Make the PR forge calls verify: single re-read helper and typed indeterminate outcome
parent: 042cxmtm4
needs: 
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
## Behaviour
A small helper in the pr command layer reads the PR after any write (ready, body edit, merge) and returns a typed outcome (`Verified`, `Unchanged`, `NotApplied`) instead of trusting the write's response. `NotApplied` maps to exit 4 for ready/merge. Backends stay free of ledger knowledge.

## Scenarios
- write accepted but PR unchanged (memory forge that ignores ready): outcome NotApplied, exit 4. Prevents: ledger and forge disagreeing silently.
- write succeeds and read shows change: Verified.

## Reference coverage
Shared by pr ready (still-draft indeterminate), pr merge (merge not visible), pr check (write not sticking): 3 reference tests.

## Qew today
Missing; qew trusts the return value of mark/merge calls.
