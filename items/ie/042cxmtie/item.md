id: 042cxmtie
kind: issue
title: Prove a draft is never ready, startable or completable, and header edits cannot release it
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: ulnyzsnt
---
## Behaviour
State comes only from the event fold. Walks must pin that every consumer agrees a draft is not workable:
`ready`, `blocked`, `start`, `evidence`, `complete`, the session-start prime and mirror board columns (Draft column
= not startable). Refusals name the way out: `qew draft approve`. A hand edit of an item header (labels such as
`qew:approved`, an `owner:` value) or a forge-side edit never changes state; `qew check` refuses a non-empty
`owner`. An open draft still blocks what needs it (a need is met only by `completed`). A draft epic can never be
completed and children of a draft epic are not released by it. `qew list` deliberately shows drafts with their
state column (the ledger is a database, not a work queue), which differs from the reference.

## Scenarios
1. A draft is absent from `qew ready` and `qew blocked` even with all needs met. Prevents unapproved work being offered.
2. `qew start DRAFT` exit 2 and message names `qew draft approve`, no claim event. Prevents starting unapproved work.
3. `qew evidence DRAFT` and `qew complete DRAFT` exit 2 naming `qew draft approve`. Prevents evidence or completion on unapproved work.
4. Header edit adding a label named like an approval to a draft (or a forge mirror file claiming approved) leaves it a draft in `list`/`ready`. Prevents the label-in-the-UI adversary: state derived from anything but events.
5. A draft that another item needs keeps that item blocked in `ready`/`blocked`. Prevents a dependent running ahead of unapproved work.
6. A draft epic is refused by `qew complete` and `qew draft approve --tree` is named as the fix. Prevents completing a plan nobody approved.
7. Session-start prime output lists approved ready work and no draft (cross-check with the hooks area). Prevents agent context offering drafts.

## Reference coverage
Reference draft-state tests: draft never ready, left out of list and prime, plan status counts a draft child and never
selects it (the plan-status half lives in plan-status-rollup), start refuses a draft and names approval, complete
refuses a draft without writing, a draft epic is never completed by plan complete (5 of 6; the sixth, the
plan status draft count, is in plan-status-rollup).

## Qew today
Covered by the state machine: a draft is not in `ready`, `start` refuses it (flow walk start refusal, golden walk
`ready` empty before approval). Missing: assertions on the approval hint text, evidence/complete on a draft, header-edit
adversary, dependent-blocked case, draft-epic complete, prime walk.
