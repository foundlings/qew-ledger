id: 042cxmtia
kind: issue
title: Prove every human-release command validates the quote before touching the ledger
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
`draft approve`, `draft revert` and `create --quote` all call the shared quote check. The guarantee to pin with
scenarios: validation runs before items are resolved or any file is written, the same refusal table applies on
every entry point, and the refusal is exit 2 with the form `Name: 'their words'` in the message. An approval with
no human words behind it must never produce an `approved` event, since only quoted words release work.

## Scenarios
1. Table walk over `draft approve`: missing flag, empty, `ok`, no name, unquoted, multi-line, placeholder (`<their words>`, dots, TODO) all exit 2 and leave the item's events as `drafted` only. Prevents agent-minted approval.
2. Same table over `draft revert` (with a valid reason) writes nothing. Prevents withdrawing approved work on an invented quote.
3. Order: a bad quote with an unknown item reference reports the quote problem first and touches nothing. Prevents partial resolution side effects.

## Reference coverage
Reference: approve `a human quote is required before any call` (1 of 14), revert `a reason and a human quote are
required before any call` (1 of 12). The reason half is in draft-revert-tree-and-reason.

## Qew today
Covered in code (shared require_quote, identical rules). Tested only for the single value `ok` on approve (flow walk); the other forms and the revert path have no test.
