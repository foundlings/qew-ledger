id: 042cxmtmg
kind: issue
title: Merge refuses every unready PR with distinct messages and exit codes, writing nothing
parent: 042cxmtm4
needs: 042cxmtmd
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: lkkplpsu
---
## Behaviour
`qew pr merge NUMBER` reads the PR once, applies the full gate in order, and only then calls the forge, pinned to the head it read (`merge_pull_request(number, head_sha)`, a merge commit, no squash). Refusals (zero writes): not open -> exit 2 (closed, merged distinguished); draft -> exit 2 with `run qew pr ready N`; conflicts -> exit 2; unknown mergeable (None) is told apart from conflicts (`merge state unknown, retry`); unticked checklist items -> exit 2 naming them; covered item still a draft -> exit 2 naming the item and `qew draft approve`; failing checks and pending checks told apart (both exit 3, texts `are failing` / `are pending`); `none` checks allowed. The success line names the SHA and the next step `qew complete ID`.

## Scenarios
- refusal table, each in its own subtest asserting code, text and zero merge calls: draft, open checklist item, draft covered item, conflict, unknown mergeable, closed, merged, failing checks, pending checks. Prevents: any unready merge.
- no checks at all may merge (just pushed, no rollup). Prevents: deadlock on repos without CI.
- golden: ready green PR merges exactly the checked head (forge sees the sha) and prints the complete hint.
- head moved after the check: forge refuses, nothing merged, error exit 1. Prevents: merging unreviewed commits.
- incomplete data about covered items or checks is an indeterminate failure exit 4 and no merge. Prevents: guessing readiness.

## Reference coverage
Reference pr merge walk file: golden, refusals-write-nothing table (9 cases), no checks may merge, failing vs pending told apart, covered draft label refusal (appears twice in the file), incomplete closing references indeterminate. About 7 test functions.

## Qew today
Reduced: `merge_pull_request` covers draft, conflict/unknown (one message, so unknown is not told apart), failing/pending (one exit 2 and message form, not distinguished by code), exact head, unrecorded; `test_merge_refuses_draft_red_conflicted_and_unrecorded_pull_requests` and the moved-head test exist. Missing: closed vs merged state messages, checklist gate (needs pr-check-command), covered-item draft check for epic PRs, golden asserting the hint text beyond 'qew complete', JSON output, indeterminate handling.
