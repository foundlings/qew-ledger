id: 042cxmtn5
kind: issue
title: Add item comments as append-only ledger events and show them on `qew show`
parent: 042cxmtmt
needs: 042cxmtmu
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew comment ITEM (--body TEXT | --body-file F)` appends a `commented` event (actor, time, body) and prints `commented on ID`. The body must be non-empty after trimming; exactly one of `--body` and `--body-file` is allowed; `-` reads stdin; the refusal happens before any write. Comments are untrusted text: `show` lists them with author and time, annotated with text findings, and routine reads never print them. Mirroring a comment to a forge is a sync concern (separate issue); the ledger record is the truth. `qew check` validates the new event type.

## Scenarios
- golden: comment with `--body` then `show --json` lists the comment with author and timestamp. Prevents discussion living only on the forge.
- golden: `--body-file` preserves the file's exact text including the final newline. Prevents silent body mangling.
- refusal: missing body, whitespace-only body, and both `--body` and `--body-file` exit 2 and write no event file. Prevents an empty or ambiguous comment.
- adversary: comment text containing a claim-marker-looking string or HTML comment is stored verbatim as data and never interpreted as a claim or release. Prevents a comment forging a state change.

## Reference coverage
Reference draft-read walk comment tests: adds the body, reads a body file, refuses missing/empty/double body (3 tests).

## Qew today
Missing. There is no comment command or comment event type; hook guard blocks forge comments but nothing replaces them.
