id: 042cxmtig
kind: issue
title: Pin the whole requester-quote refusal table on every entry that takes a quote
parent: 042cxmti7
needs: 042cxmtia
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: vuvqukwu
---
## Behaviour
Quote rule (shared module, identical to the reference): `Name: 'their words'` on one line, name present, at least
12 characters of words, no placeholder (only dots or ellipses, `<...>`, TODO, TBD, placeholder, his/her/their
words). Entry points in the ledger: `qew create --quote`, `qew create --from-file` (global and per-item),
`draft approve`, `draft revert`, and the apply path. Refusal is exit 2 before any item or event file is written.
Behaviour that differs by design and is recorded here: in the ledger a draft needs no quote (an agent may file
drafts freely); the quote is what releases work.

## Scenarios
1. `create --quote` table: empty, too short, no name, unquoted, placeholder, dots, TODO, multi-line each exit 2 and the ledger gains no file. Prevents an unattended agent satisfying the gate with junk.
2. `create` with no quote files a draft and writes `drafted`; with a valid quote files `approved` carrying the exact trimmed quote. Prevents approved work with no trace of the requester.
3. `create --from-file` applies the single `--quote` to every item or none (all-or-nothing validation before the first write). Prevents half a file approved.

## Reference coverage
Reference requester-quote tests merged: create without quote refused before any write, create refuses empty/short/
unattributed/placeholder quotes (8 subcases), create renders the quote and waits for approval by default (the
quote half; the approval gate half is dropped), plan create requires and renders the quote (quote half) - 4 of 9.

## Qew today
Code shared and correct. Test coverage: only `ok` on approve and the happy-path `--quote` on create. The eight-form table is untested.
