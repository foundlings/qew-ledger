id: 042cxmtmw
kind: issue
title: Prove `qew ready` excludes everything that is not startable, in one scenario per class
parent: 042cxmtmt
needs: 
labels: area:read-side
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: swlnmnxn
---
## Behaviour
Ready means: approved (a human's quote exists), unclaimed, not an epic, not a draft, not closed or completed, and every need completed. The reference proves each class is held back, including the rule that an unrelated gate outranks claim and blocker so a human sees that a decision is owed. In the ledger the equivalent gates are: draft (never ready even if a later `field` event or label looks like approval), reverted work (back to draft), claimed work, a need that is open, claimed, draft, closed (closed does not count as done) or dangling, and an epic (only its children are ready). The derived answer must not depend on label spelling or on forge state.

## Scenarios
- golden: a ledger with ready, claimed, blocked, draft, epic, completed and closed items lists only the ready ones, in priority order. Prevents a dispatcher starting claimed or unapproved work.
- adversary: a draft item whose labels include the word approved (a human edited labels by hand) is still not ready. Prevents label text standing in for a quoted approval.
- adversary: item whose need is closed as not_planned or whose need id is dangling stays out of ready. Prevents guessing a ready state from missing data.
- golden: completing the only open need makes the dependent appear in `qew ready` on the next run with no other action. Prevents a stale cached readiness.

## Reference coverage
Reference ready walk: approval-gated work is never ready; golden walk lists only actionable work (open blockers and assignees keep work out). Reference model-output walk: case-insensitive label handling and epic excluded from ready. 4 tests; the truncated-blocker refusal test is dropped as forge-pagination only (see dropped).

## Qew today
Partially covered by `test_golden_walk_from_draft_to_ready_to_blocked` and `test_start_refuses_drafts_double_claims_and_blocked_work`; no dedicated exclusion matrix for epic, closed need, dangling need, reverted work or hand-edited labels.
