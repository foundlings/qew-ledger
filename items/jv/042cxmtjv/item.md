id: 042cxmtjv
kind: issue
title: Record that release verification is local, not a forge workflow
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: uzwmuzkn
---
## Behaviour
Spec-only: docs/specs/releases.md already states no workflows. Add the pointer that the two reference workflow assertions (tag checkout uses event sha) live in the local release script issue.

## Scenarios
None.

## Reference coverage
test_checkout_uses_the_event_commit_not_the_movable_tag.

## Qew today
Decided in docs/specs/releases.md.
