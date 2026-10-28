id: 042cxmtmz
kind: issue
title: Annotate `qew list` rows with a derived work state and order by actionability
parent: 042cxmtmt
needs: 042cxmtmy
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: tyqqmllz
---
## Behaviour
Beyond lifecycle state, list rows carry a derived `work_state`: `ready`, `claimed`, `blocked`, `plan` (epic), `needs_decision` (a draft awaiting a human) and `closed`/`completed`. Default order is actionable first: ready, then blocked, then claimed, then plans, then the rest; within a class priority then id. A stuck item that is both claimed and blocked reports the more urgent class deterministically (documented). `--state` still filters on lifecycle state; `--work-state` filters on the derived class.

## Scenarios
- golden: a ledger with a ready item, a claimed item, a blocked item and an epic prints `ready, claimed, blocked, plan` work_state values in the documented order. Prevents agents scanning past noise to find work.
- adversary: an item that is claimed and has an unmet need reports one documented work_state, not two or none. Prevents ambiguous automation.
- golden: draft-awaiting-decision rows appear after blocked work and before closed. Prevents a pending human gate being hidden below completed history.

## Reference coverage
Reference read-suite walk: list orders and annotates work states; shows approval-gated work after blocked; reports stuck gated work as needs_approval (3 tests). The projection test (the query must fetch the fields work state needs) is forge-query-shaped and is dropped.

## Qew today
Missing. Rows show lifecycle state only.
