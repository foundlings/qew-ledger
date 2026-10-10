id: 042cxmtkb
kind: issue
title: Land refuses unsafe cases: other actor's claim, unmerged, wrong base, bad data
parent: 042cxmtjw
needs: 042cxmtk7 042cxmtk3
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: vokrmouv
---
## Behaviour
Adversary walks for `qew land`: another actor's claim is reported with the exact `qew complete ITEM --take-over` command and never touched (exit 0); an unmerged or closed PR is a quiet no-op (exit 0); an item whose pull request merged into a non-target branch (a stacked branch) is reported `still open` and left alone because the merge is not on the configured target; an unreadable or truncated list of linked items, or a merged PR without a valid merge commit id, is indeterminate (exit 4) and writes nothing; a non-positive or non-numeric PR number is exit 2 before any ledger or forge access.

## Scenarios
- another actor's claim: reported with take-over command, zero events (prevents: automation silently taking over a teammate's claim)
- PR not merged: `not merged`, exit 0, zero events
- merge into a stacked (non-target) branch: item reported open and untouched (prevents: completing work that has not reached the target)
- truncated link data or invalid merge sha: exit 4, zero events (prevents: landing on guessed data)
- PR number 0, -3, `abc`: exit 2, no access (prevents: argument confusion)

## Reference coverage
6 reference test function(s): `test_another_logins_claim_is_reported_never_touched`, `test_an_unmerged_pull_request_is_a_quiet_no_op`, `test_an_issue_github_left_open_is_left_alone`, `test_truncated_closing_references_are_indeterminate`, `test_a_merged_pull_request_without_a_valid_merge_commit_is_indeterminate`, `test_a_non_positive_pull_request_number_is_refused_before_any_call`

## Qew today
Missing, with the command.
