id: 042cxmtn2
kind: issue
title: Make `qew show` report related items with state and title, plus the next workable child of an epic
parent: 042cxmtmt
needs: 042cxmtmu
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`show` prints and returns: header fields, state, owner, `blocked_by` and `blocking` as objects `{id, state, title}` (not bare ids), `parent` and `children` the same way, evidence, mirrors, comments (see item-comments), body. For an epic it names `next`, the highest-priority ready child (id, priority, title), in the text form as `next: ID pN title`. Related items are looked up locally so a dangling edge is reported as `missing` rather than hidden. Unknown reference exits 2; ambiguous short alias lists the candidates.

## Scenarios
- golden: show of an item with a need, a dependent, a parent and a child prints each with state and title in JSON. Prevents an agent opening four more items to understand one.
- golden: show of an epic with two approved children names the lower-priority-number child as `next`. Prevents agents guessing where to start.
- refusal: show of an unknown or ambiguous reference exits 2 and names the candidates. Prevents acting on the wrong item.
- adversary: a need that no longer exists prints `missing`, not an empty slot. Prevents a hidden dangling edge.

## Reference coverage
Reference read-suite walks: show golden walk exposes only the numbered issue (blocked_by, blocking, parent, children, comments); show plan names its next workable child (2 tests).

## Qew today
Reduced. Show prints ids only for needs/children/blocks, no titles or states, no `next`. Covered: `test_show_resolves_a_short_alias_and_reports_derived_edges`.
