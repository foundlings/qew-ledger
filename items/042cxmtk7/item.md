id: 042cxmtk7
kind: issue
title: Add `qew land PR` to complete the caller's claimed items after a pull request merges
parent: 042cxmtjw
needs: 042cxmtk2 042cxmtk0
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: vokrmouv
---
## Behaviour
After a pull request merges, `qew land PR_NUMBER [--target T] [--json]` completes the items it delivered. Items come from the ledger's own `pr` mirror records for that pull request (and the items linked by `qew pr open`), never from PR title or body text (untrusted). Each such item still claimed by the caller is completed exactly as `qew complete` would, with the merge commit (pinned in the pr mirror or read from the forge) as landing proof; `--json` prints `{state, landed, held, clean}`. Idempotent and safe from a hook: a second run finds nothing to do and exits 0.

## Scenarios
- golden: merged PR delivers item A claimed by me; A is completed with the merge commit as evidence and output names `landed A from PR N` (prevents: a merge that leaves a stale claim)
- mixed json: one landed, one held by another actor, one already completed: `landed`, `held` (with holder), `clean` lists are exact (prevents: callers parsing prose)
- second run: `nothing to land`, exit 0, zero events (prevents: duplicate completion on retry)
- items taken from a PR body that names an unrelated item id are ignored (prevents: closing work from attacker-controlled text)

## Reference coverage
3 reference test function(s): `test_golden_walk_completes_the_callers_stale_claim_with_the_merge_commit`, `test_json_reports_landed_held_and_clean_issues`, `test_already_clean_issues_are_left_alone`

## Qew today
Missing. `qew pr merge` merges and prints a pointer to `qew complete`; nothing completes items from a merged pull request.
