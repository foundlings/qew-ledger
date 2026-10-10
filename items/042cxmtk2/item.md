id: 042cxmtk2
kind: issue
title: Record the reason, the full commit and the merged pull requests on `completed`
parent: 042cxmtjw
needs: 042cxmtk0
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lyrtzqmu
---
## Behaviour
`qew complete ITEM --reason TEXT` appends a `completed` event carrying the reason, the full commit ids proven landed on the target branch (shortened input is resolved to the full id) and the numbers of merged pull requests recorded in the item's `pr` mirrors for those commits (reference closing comment: `Landed: commit <sha> on <branch>`, `PR: #N`). `qew show` prints it. Input defences before any read or write, exit 2: empty or whitespace reason; a change id that is not hex/jj id (covered by `valid_change`); a branch name that is empty, starts with `-` or contains `...`. `--landed-on BRANCH` may override the configured target for stacked branches. The tip itself counts as landed.

## Scenarios
- golden: evidence on target, reason given; event holds reason, full sha, branch and merged PR numbers; show prints them (prevents: completion with no audit of what landed)
- tip of the target branch is accepted as landed (prevents: refusing the commit that just merged)
- hostile branch or change values (`main...evil`, `-x`, `not-a-sha`, blank reason): exit 2, zero events, no VCS command run (prevents: option injection into git or jj)
- behind/diverged commit: refused naming change and target (covered by flow walk test_complete_is_refused_when_evidence_is_not_on_the_target_branch)

## Reference coverage
3 reference test function(s): `test_complete_records_a_commit_proven_on_the_landing_branch`, `test_complete_accepts_the_branch_tip_itself`, `test_complete_refuses_a_commit_that_is_not_on_the_branch`

## Qew today
Reduced. Ancestor check against the configured target and jj/git are covered (flow walk, including the jj change-id walk). Missing: reason, full-sha normalisation, PR numbers, `--landed-on`, hostile-value tests (the code rejects leading `-` in target but has no test and no `...` rule).
