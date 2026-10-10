id: 042cxmtkq
kind: issue
title: Add `qew comment ITEM` as an append-only comment event
parent: 042cxmtjw
needs: 
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: zmpyzrrm
---
## Behaviour
`qew comment ITEM (--body TEXT | --body-file FILE)` appends a `comment` event with the text and the actor (CLAUDE.md names `qew comment` for discussing drafts). Exactly one of body and body-file; empty or whitespace-only is refused; a symlinked body file is refused; text is stored as data, size-bounded, and never evaluated. Works on any state including draft, completed and closed. `qew show` prints the ten most recent comments (and `--json` all of them), truncating with a count. Event schema gains `comment` (allowed in every state, no transition).

## Scenarios
- golden: comment on a draft; show lists it with actor and time (prevents: draft discussion lost in chat)
- both or neither of `--body` and `--body-file`, empty text, symlinked file, oversize text: exit 2, no event (prevents: junk and path tricks)
- comment with text that looks like a command or an event JSON: stored verbatim, nothing executed (prevents: treating comments as instructions)
- two branches each add a comment: merge keeps both (prevents: lost discussion)

## Reference coverage
No dedicated reference test; specified from the reference command documentation. (spec) comment command; no dedicated reference walk in scope

## Qew today
Missing. No command and no event type.
