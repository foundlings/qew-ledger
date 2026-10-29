id: 042cxmtn6
kind: issue
title: Make `qew show` and epic progress say when an item is a draft
parent: 042cxmtmt
needs: 042cxmtn2
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: yqnpnuuzymmv
---
## Behaviour
The first show line names the state so a draft is never read as live: `ID draft ...` versus `ID approved ...` (the ledger state is already authoritative; the first line must carry it with kind and title). JSON carries `draft: true|false`. Epic progress text counts drafts separately (`0/3 completed, 2 drafts`); a draft epic reports `(draft epic)`, is never offered as completable, and its completion command is null. Output for live work is unchanged and has no draft wording.

## Scenarios
- golden: show of a draft prints the word draft in line one; show of approved work does not. Prevents a reader treating drafts as live.
- golden: epic progress with two draft children and one live child reports the draft count. Prevents `0/3` hiding unseen drafts.
- adversary: an epic that is a draft whose children are all completed is never offered `qew complete` and says it is a draft. Prevents a refused command being advertised.
- golden: progress text without drafts is byte-identical to before. Prevents regressions for existing consumers.

## Reference coverage
Reference draft-read walk `show reports whether the issue is a draft` and draft-text walk (show says draft; live unchanged; plan status counts drafts; draft plan never completable; text without drafts unchanged): 6 tests. The epic-progress command itself belongs to the plan/epic area; coordinate there.

## Qew today
Reduced. `show` prints `state:` but no draft boolean in JSON and no epic progress line.
