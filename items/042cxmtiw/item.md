id: 042cxmtiw
kind: issue
title: Validate actor identity written into events and refuse unsafe values
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Reference refuses a viewer login that cannot be a label (GitHub text is untrusted) and refuses a hand-written
`author:` area. Ledger: the actor recorded in events (`QEW_ACTOR`, else `USER`, else `unknown`) is untrusted
environment text. It must be a single-line token without whitespace or commas, otherwise the command refuses
(exit 3, environment) before writing; `qew check` flags events whose actor is not such a token. The author is
derived from the first event, never settable through `--label author:...`-style input; claiming is by event, never
by header.

## Scenarios
1. `QEW_ACTOR="bad login,x"` makes `create`/`start` exit 3 with no file written. Prevents a malformed identity reaching event files and later forge labels.
2. Newline in the actor value refused. Prevents forged extra lines in rendered output.
3. A label `author:mallory` is accepted as an ordinary label but never changes the derived author or owner. Prevents forged attribution.

## Reference coverage
Reference graph-write: create labels work with the author who opened it (and never assigns), creates a missing author
label, refuses a hand-written author area, refuses an unsafe viewer login (4 of 26). Label creation and assignee
behaviour are forge-sync concerns (see dropped).

## Qew today
Missing: `actor()` returns the environment value unchecked.
