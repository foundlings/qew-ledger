id: 042cxmtng
kind: issue
title: Keep own comments, bots, machine markers and out-of-window comments out of the inbox
parent: 042cxmtmt
needs: 042cxmtnf
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
A reply is a comment by someone other than the viewer, not by a bot (actor type bot or a `[bot]` suffix), not a machine marker (claim or release markers written by qew itself), and at or after the window start (inclusive). Comparison of logins is case-insensitive. Excerpts replace control characters with spaces so item text never reaches the terminal raw.

## Scenarios
- adversary: own comments, a bot actor, a `[bot]` login, claim/release markers, and a comment one second before the window all yield no reply; a comment exactly at the window start does. Prevents inbox flooding.
- adversary: a comment containing escape sequences and newlines prints with those replaced by spaces in text output. Prevents terminal injection.

## Reference coverage
Reference inbox walk: self, bot, marker and old comments are not replies (1 test) plus printable excerpt handling in the golden walk.

## Qew today
Missing.
