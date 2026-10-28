id: 042cxmtm8
kind: issue
title: Open PRs for draft items without a claim; always a forge draft, refuse `--ready`
parent: 042cxmtm4
needs: 042cxmtm5
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
## Behaviour
A PR may be opened for a draft item (a plan's epic pull request opens at planning time when nobody can claim anything). It needs no claim, is always a forge draft, and `--ready` on a draft item is refused (exit 2, message says the PR is always a draft) before any forge call. For approved items `--ready` opens non-draft. In the ledger model the 'PR is held back' state is DERIVED from the covered items' folded states (any covered item draft => PR is held), never stored as a forge label; the forge-side marker (title prefix or a label where the forge has labels) is a best-effort mirror only.

## Scenarios
- draft item, no claim: `qew create --draft` item + `qew pr open` -> draft PR, mirror written. Prevents: forcing a human approval or fake claim just to open planning work.
- `--ready` on a draft item: refused exit 2, no forge call, no mirror. Prevents: a plan PR visible as reviewable while its issues are unapproved (reference returned exit 2).
- approved unclaimed item opens a draft by default and non-draft with `--ready`. Prevents: accidental ready PRs.

## Reference coverage
Reference draft-PR walk file: opening a PR for a draft issue needs no claim and marks the PR as held; ready refused for a draft issue. 2 test functions.

## Qew today
Reduced: `open_pull_request` computes `draft = not ready or state == DRAFT`, silently downgrading `--ready` instead of refusing it. The 'no claim needed' half works because open never checks a claim; no test pins it. Terminal items (completed/closed) are refused already.
