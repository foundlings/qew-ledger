id: 042cxmtkm
kind: issue
title: Accept `qew create --draft` and refuse contradictions with `--quote`
parent: 042cxmtjw
needs: 
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lkpulxlt
---
## Behaviour
The project rules and the reference name `create --draft` explicitly. In qew a create without `--quote` is already a draft, but the flag does not exist, so the documented invocation fails. Add `--draft` as an explicit statement of intent: it files a draft (`drafted` event, never `approved`), and combined with `--quote` it is a usage error (exit 2, before any write) instead of silently choosing one meaning. Epic drafts: `qew create --kind epic --draft`; a draft epic accepts `--parent` for itself but the plan-create rule `no --children on a draft plan` belongs to the plan area.

## Scenarios
- `create --draft`: item is draft, never ready or startable, event is `drafted` only (prevents: draft treated as live work)
- `create --draft --quote Q`: exit 2 naming both flags, zero files (prevents: contradictory flags silently approving)
- draft epic with draft children via `--parent`: whole subtree drafts (prevents: mixed states under one plan)

## Reference coverage
2 reference test function(s): `test_create_draft_files_work_marked_draft_and_never_approved`, `test_draft_with_approved_or_needs_approval_is_refused_before_any_call`

## Qew today
Reduced. Draft is the default and covered by ledger walk test_golden_walk_from_draft_to_ready_to_blocked (`drafts are never ready`), but `--draft` is rejected as an unknown argument.
