id: 042cxmtib
kind: issue
title: Add `--tree`, skipping and reason validation to `qew draft revert`
parent: 042cxmti7
needs: 042cxmtia
labels: area:drafts-plans
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew draft revert ITEM... [--tree] --reason TEXT --quote Q` returns approved, unclaimed work to draft.
- `--reason` must be non-blank. Today `--reason " "` passes the CLI and the event parser (it only rejects the
  empty string), so a revert with no explanation is recorded.
- `--tree` includes open descendants; items already in draft or closed are passed over and reported as skipped;
  the one-visit rule and the single refusal for the whole tree (see draft-revert-guards) apply.
- A lone item that is a draft is refused with `nothing to revert`; in a mixed list it is skipped and reported.
- A closed item is refused before any write. Duplicate references collapse to one target.
- Revert is the exact inverse: a later `draft approve` of the same item works and the fold is
  approved - draft - approved with both quotes kept in the event history.
- Output `ID draft` per item and `--json` `{"reverted": [...], "skipped": [...]}`.

## Scenarios
1. Golden: revert one approved item with reason and quote; event `reverted` carries both, state is draft, `qew ready` no longer lists it. Prevents live work staying startable after withdrawal.
2. Tree: epic approved with an approved child, a draft child and a closed child; `--tree` reverts epic and approved child, skips the draft, ignores the closed one. Prevents half the tree staying live.
3. Blank reason (`' '`, missing) exit 2, nothing written. Prevents an unexplained withdrawal.
4. Lone draft refused `nothing to revert`; mixed list skips it. Prevents erroring on a rerun and prevents silent no-ops.
5. Closed item refused, nothing written. Prevents reopening discarded work as a draft.
6. Round trip revert then approve then start works; dependents of the reverted item stay blocked while it is a draft. Prevents lossy round trips and a dependent running ahead of its blocker.
7. Duplicate references `A A` produce one event; `qew check` passes. Prevents an illegal second `reverted` event.

## Reference coverage
Reference revert tests merged here: golden, tree reverts live descendants and skips drafts and closed, closed work
refused, lone draft refused and mixed skipped, reason and quote required (partially), approval gate survives the
round trip (the part about dependents and reapproval; the needs:approval label itself is dropped) - 6 of 12 revert
tests.

## Qew today
Covered: single revert of approved unclaimed work (flow walk `draft_revert_returns_unclaimed_work_to_draft_only`),
quote required, claimed work refused via the transition table.
Missing: `--tree`, skipped reporting, blank-reason refusal (verified gap: only the empty string is rejected),
nothing-to-revert wording, JSON output, duplicate collapse, round trip test.
