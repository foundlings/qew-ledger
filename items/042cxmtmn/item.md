id: 042cxmtmn
kind: issue
title: Support plan epic PRs: one PR covering an epic and its descendants
parent: 042cxmtm4
needs: 042cxmtm8 042cxmtm9
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
A PR may cover several items (an epic and its children). The pr mirror records the covered item ids at open time (all descendants not closed, or an explicit list); ready/merge/check compute readiness over ALL covered items: while any is a draft the PR is held (ready and merge refused exit 2, naming the draft items); after `qew draft approve --tree` the same PR becomes readyable with no forge-side edits. `draft revert` of a covered item with an open non-draft PR is refused (exit 2); with a draft PR it stays draft. The hold is derived from ledger state so it cannot drift from a forge label.

## Scenarios
- plan PR for a draft epic: open, ready refused, merge refused while any child is draft. Prevents: merging a plan before approval.
- partial approval: approve one of two children, PR still held naming the other. Prevents: early merge.
- full approval: `draft approve --tree` then `qew pr ready` and merge succeed without extra steps. Prevents: stuck PRs.
- revert with a ready PR refused; revert with a draft PR allowed and PR stays held. Prevents: a live PR for work that went back to draft.
- forge marker best-effort: where the forge supports labels, sync keeps a `draft` marker consistent; failure to sync it is a warning naming the manual fix, never the truth.

## Reference coverage
Reference draft PR walk file: approve removes the label, label stays while another closing issue is draft, revert adds the label, ready PR still blocks revert, ready refused while labelled draft; merge walk label refusal (twice). About 7 test functions mapped (2 for open covered by pr-open-draft-item).

## Qew today
Missing: a pr mirror covers exactly one item, no tree, no held-state derivation, no revert interaction. `cmd_draft` does not look at pr mirrors.
