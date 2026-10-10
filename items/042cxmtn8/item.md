id: 042cxmtn8
kind: issue
title: Add `qew search TERMS` over approved work with best-match order and capped warning
parent: 042cxmtmt
needs: 042cxmtmu
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: kuzsrksvxzyo
---
## Behaviour
`qew search TERM...` is a local, offline substring search over ids, titles and labels of approved, non-draft items (all words must match, case-insensitively). Bodies and comments are never searched or printed by `search`; draft and unapproved text is reachable only through `triage`. Results are ordered by match quality (exact title match, then word-boundary, then substring) then priority then id. A cap (default 30, `--limit`) prints a stderr warning `search results capped`. An empty result prints a one-line hint on stderr to try `qew triage --search`. Search terms are data: never evaluated or passed to a shell.

## Scenarios
- golden: two approved items and one draft match the term; the output lists the two approved, best match first, and not the draft. Prevents unapproved text surfacing through a routine read.
- golden: more matches than the cap prints the capped items and a stderr warning. Prevents a silently clipped answer.
- golden: no match exits 0, prints nothing, and the stderr hint names `qew triage --search`. Prevents a dead end.
- adversary: a term carrying shell metacharacters, newlines or a leading dash is matched literally and executes nothing. Prevents injection through the query.

## Reference coverage
Reference read-suite walks: search golden (vetted, best-match order) and search warns when capped and hands empty results to triage (2 tests). The search-term-as-GraphQL-variable rule is forge-only and is dropped; the ledger form is `terms never reach a shell`.

## Qew today
Missing. No search command.
