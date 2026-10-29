id: 042cxmtio
kind: issue
title: Pin epic completion walks: draft epic, open children, idempotent rerun
parent: 042cxmti7
needs: 042cxmtin
labels: area:drafts-plans
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: ulnyzsnt
---
## Behaviour
The ledger has no separate plan-complete verb: `qew complete EPIC` does it (claimed epic, every child completed
or closed, at least one child, no evidence of its own). Remaining reference guarantees to pin or add:
- Draft epic refusal names `qew draft approve` (today the generic not-claimed text is shown).
- Open children refusal names the count (`1 child remains open`) and lists the ids.
- Re-running `qew complete` on an already completed epic is a clear no-op or a precise refusal naming state
  completed; it never appends a second `completed` event (illegal transition makes `check` fail).
- A child that is a draft blocks completion like any open child.
- A closed-not-planned child counts as done; an epic closed instead of completed is not completable.

## Scenarios
1. Golden: claimed epic, all children completed: complete succeeds, JSON-free output `ID completed`. Prevents plan closing needing manual checks.
2. One open child: exit 2 with count and id, no event. Prevents closing a plan with live work.
3. Draft epic: exit 2 naming `qew draft approve`. Prevents completing an unapproved plan.
4. Draft child under an approved epic blocks completion. Prevents hiding unreleased work.
5. Second `qew complete` on a completed epic writes nothing and `qew check` passes. Prevents an illegal duplicate event.

## Reference coverage
Reference plan-status tests: plan complete golden walk verifies all children then closes, refuses an open child without
writing (2 of 6); draft-state: a draft epic is never completed by plan complete (1 of 6).

## Qew today
Covered: golden epic completion and no-children refusal (flow walk), unfinished-children refusal in code. Missing: draft epic hint, rerun, draft child and a test per message.
