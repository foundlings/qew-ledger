id: 042cxmtnh
kind: issue
title: Validate inbox --since and --login, with documented defaults and no qualifier injection
parent: 042cxmtmt
needs: 042cxmtnf
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`--since` is a UTC instant `YYYY-MM-DDTHH:MM:SSZ` or a date (midnight UTC); anything else (yesterday, impossible dates, offsets, space separator, empty) is a usage error (exit 2) before any read. Default window is the last 7 days relative to now with no persisted state. `--login` defaults to the configured actor (git/jj identity or env); a login must match the forge login charset (letters, digits, hyphen, optional `[bot]`) so it can never smuggle a query qualifier into a forge-side lookup. These shared instant helpers live in one small module, also used by timestamps in events (invalid event time is a loud ledger error).

## Scenarios
- refusal: five malformed `--since` values each exit 2 and read nothing. Prevents a wrong window silently dropping replies.
- golden: `--since 2026-10-07` is midnight UTC and the output header says so. Prevents timezone ambiguity.
- golden: with no flags the window is seven days and the login is the configured actor. Prevents an unscoped inbox.
- adversary: `--login 'alice label:secret'` exits 2 before any read. Prevents qualifier injection when the inbox is mirrored to a forge query.

## Reference coverage
Reference inbox walks: malformed since is usage error; date since means midnight UTC; defaults to authenticated user and seven days; login cannot inject search qualifiers (4 tests).

## Qew today
Missing.
