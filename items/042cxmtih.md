id: 042cxmtih
kind: issue
title: Show who asked for an item and why it was released or withdrawn
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
The reference writes the quote into the issue body under `## Requested by` so a reader sees who wanted the work.
In the ledger the quote lives in the `approved`/`reverted` events; it must be readable without opening event files:
- `qew show ID` prints `released: Name: 'words'` (latest `approved` event, actor, time) and, after a revert,
  `withdrawn: reason` with the reverting quote; `--json` has `approvals` as a list of
  `{type, at, actor, quote, reason}`.
- `qew show` marks drafts: first line state `draft`; live work unchanged.
- Mirror bodies end with the `## Requested by` block from the latest approval (a cross-area requirement for the
  sync area; this issue only pins the data `show`/`--json` expose and the rendering helper).

## Scenarios
1. Show of an approved item prints the exact quote and approver. Prevents work with no visible requester.
2. Show of a reverted item prints the reason and the reverting quote and state draft. Prevents an unexplainable revert.
3. Show of a plain draft says draft; show of approved unchanged apart from the released line. Prevents a draft being indistinguishable.

## Reference coverage
Reference: show reports whether the issue is a draft (JSON key and text `#5 open draft`), show of live work unchanged
(3 of 8 draft-read and draft-text), create renders quote (1 of 9). The `unrecorded` comment recovery path of the
approve command is dropped.

## Qew today
Missing: `qew show` prints state, owner, evidence and mirrors but no approval quote or revert reason; JSON has no approvals.
