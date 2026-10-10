id: 042cxmtnf
kind: issue
title: Add `qew inbox`: replies, drafts waiting for a human, and claimed work for a person
parent: 042cxmtmt
needs: 042cxmtn5 042cxmtmu
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: rumoopxukttr
---
## Behaviour
`qew inbox [--login NAME] [--since INSTANT] [--json|--count]` answers what waits on a person from the ledger alone. Replies: items the person is involved in (created, claimed, or commented) with `commented` events by someone else inside the window, each with author, time and a first-line excerpt (printable chars only, at most 100 with an ellipsis). Waiting for a human: drafts and decision-gated items the person authored. Assigned: items currently claimed by the person. Text output has fixed section headings with counts; `--json` is NDJSON rows with `section` and `schema_version`; `--count` is one line for session hooks: `qew inbox (NAME): N issue(s) with replies since T: ID (author), ...; M waiting for a human; K assigned.` and omits the list when there are no replies.

## Scenarios
- golden: replies from two authors on an item, plus one waiting draft and two assigned items, produce the three sections in order, excerpts cut to the first line and 100 characters. Prevents a person reading entire threads.
- golden: text output names each section with counts and exact lines. Prevents format drift for scripts.
- golden: `--count` is a single line listing reply items with the last author; with no replies the list is omitted. Prevents a noisy session start.
- golden: `qew inbox --count` output can be embedded into the session-start hook context within its byte bound. Prevents a second unbounded channel.

## Reference coverage
Reference inbox walks: golden walk; text output names each section; count is one line for a session hook; count with no replies omits the list (4 tests).

## Qew today
Missing. No inbox command, no comment events, no person view.
