id: 042cxmtk8
kind: issue
title: Report claims whose pull request already merged or whose item is finished elsewhere
parent: 042cxmtjw
needs: 042cxmtk7
labels: area:lifecycle
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
In the reference, a merge that never passed through an agent closes the forge issue but leaves a claim and a Done card. In the ledger the claim lives in events, so the equivalent stale state is: an item still `claimed` while a recorded `pr` mirror for it is merged (observed by `qew pr merge`/`qew sync`, or by a `merged` field written into the pr mirror), or a claimed item with no activity beyond a configured age. `qew check` prints a non-fatal note `claimed but its pull request merged: IDS` with the fix command (`qew land PR`), `qew list --state claimed --json` may carry a `stale` flag, and nothing is written. Open claimed items with no merged pull request and completed items are never stale.

## Scenarios
- claimed item whose pr mirror is merged: reported with `qew land` fix, exit 0, nothing written (prevents: leftovers nobody sees until a board disagrees)
- completed item and a claimed item with an open pull request are not reported (prevents: false alarms)
- report is shown in the human output even when `qew sync --dry-run` says mirrors are in sync (prevents: hidden stale claim because everything else looks fine)
- assignee-only variant (closed but still assigned) is dropped: assignees are not stored in the ledger

## Reference coverage
4 reference test function(s): `test_closed_issue_with_an_in_progress_label_is_reported_with_the_fix`, `test_closed_issue_with_an_assignee_is_reported`, `test_clean_closed_and_open_claimed_issues_are_not_stale`, `test_human_output_lists_stale_claims_even_when_the_board_is_in_sync`

## Qew today
Missing. `qew check` has notes only for imported-without-evidence; pr mirrors do not record merge state.
