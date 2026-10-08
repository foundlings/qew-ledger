id: 042cxmtif
kind: issue
title: Add `qew comment` so drafts and any item can be discussed without changing state
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Drafts are filed to be discussed. The ledger needs an append-only `comment` event (new type in ledger.md;
legal from every state including draft and closed) written by `qew comment ITEM (--body TEXT | --body-file F)`.
Exactly one body source is required and must be non-blank; `-` reads stdin. The event stores the text as data
only (never executed or turned into a path), shows in `qew show` in order with its actor and time, and does not
change the fold. Mirrors may render comments; that belongs to sync.

## Scenarios
1. Golden: comment on a draft appends a `comment` event, output `commented ID`, state still draft. Prevents discussion needing a state change.
2. `--body-file` and stdin variants store the file text verbatim. Prevents a quietly altered body.
3. Missing, blank, or both `--body` and `--body-file`: exit 2, nothing written. Prevents a comment that silently drops its body.
4. Comment on completed and closed items works and `qew check` still passes. Prevents the audit trail being frozen by state.

## Reference coverage
Reference draft-read tests: comment adds the body, comment reads a body file, comment refuses missing/empty/double
body before any call (3 of 8).

## Qew today
Missing: no `comment` command and no `comment` event type in `ledger_event.py`; the spec's event list has none.
