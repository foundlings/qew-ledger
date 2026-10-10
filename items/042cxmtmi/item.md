id: 042cxmtmi
kind: issue
title: Add `--json` to `qew pr open|ready|merge` with a stable schema
parent: 042cxmtm4
needs: 042cxmtmh
labels: area:pull-requests
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Machine-readable result: merge -> `{merged: true, number, head_sha, items: [IDs], schema_version}`, ready -> `{number, ready, changed}`, open -> see pr-open-golden. Every flag is in help_text, README and commands.md, per repo rules.

## Scenarios
- merge json reports merged, number, head and covered items. Prevents: agents scraping text.
- help/README/spec agree for the new flag (existing help walk fails otherwise).

## Reference coverage
Reference pr merge walk (json reports merge and what landed), pull-request walk (trailing machine flag): 2 test functions merged here.

## Qew today
Missing: only plain lines are printed.
