id: 042cxmtko
kind: issue
title: Warn on unmarked code-shaped text in an item body without altering it
parent: 042cxmtjw
needs: 
labels: area:lifecycle
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: lkpulxlt
---
## Behaviour
When a body (or comment) contains command-, flag- or path-shaped text that is not inside backticks or a fence, `create`, `set --body` and `comment` print `warning: unmarked code-shaped text: X` on stderr per finding and write the body byte-for-byte as given (exit 0). It is a hint, not a gate.

## Scenarios
- body with `qew ready --limit 5` and `./plans/work.jsonl` unmarked: one warning per token, stored body identical (prevents: later renderers or agents mistaking prose for commands)
- same text inside backticks or a fence: no warning (prevents: noise training users to ignore it)

## Reference coverage
1 reference test function(s): `test_create_warns_about_unmarked_code_without_altering_body`

## Qew today
Missing.
