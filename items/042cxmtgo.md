id: 042cxmtgo
kind: issue
title: Pin epic completion refusals and idempotence as the campaign-complete walk
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Completing an epic (`qew complete EPIC`) is the qew form of closing a milestone. Walks to add: golden complete of an epic whose children are all done (no own evidence); refusal with a count when children are open ('1 open child'), written nothing; refusal for an epic with no children ('no completed work'); completing an already completed epic is a quiet no-op with `changed: false` rather than an error or a second event; duplicate-title ambiguity does not arise because epics are addressed by id.

## Scenarios
- `epic_completes_over_finished_children_and_is_verified`: complete then show reports completed; prevents an unverified state change.
- `epic_with_open_children_is_refused_without_writing`: message counts open children; no event file added.
- `epic_without_children_is_refused`: prevents completing an empty plan.
- `completing_a_completed_epic_is_a_no_op`: second call writes no event and says unchanged.

## Reference coverage
Tests: campaign complete golden walk (changed true, state closed), campaign complete refuses open attached work without writing. The empty and repeat cases come from the implementation.

## Qew today
Partly covered: tests/test_flow_walk.py `test_an_epic_completes_over_finished_children_without_its_own_evidence`, `test_complete_is_refused_over_unfinished_child_tasks`. Missing: empty-epic refusal wording walk and idempotent repeat (verify current behaviour, then pin).
