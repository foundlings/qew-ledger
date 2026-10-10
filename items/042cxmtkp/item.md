id: 042cxmtkp
kind: issue
title: Record the item an issue was discovered while working on
parent: 042cxmtjw
needs: 042cxmtkh
labels: area:lifecycle
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew create --discovered-from ITEM` stores the origin as a `discovered_from` relation (a fixed optional header key or a first `discovered` event; the header schema rejects unknown keys, so it must be added deliberately), shown by `qew show` as a derived `discovered:` line on the origin. It is not a dependency and never blocks readiness. Unknown origin is refused before any write.

## Scenarios
- golden: item filed with an origin; show of both ends mentions the link, readiness unaffected (prevents: provenance lost in free text)
- unknown or self origin: exit 2, zero files

## Reference coverage
1 reference test function(s): `test_create_golden_walk_composes_approved_work`

## Qew today
Missing.
