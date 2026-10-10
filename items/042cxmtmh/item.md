id: 042cxmtmh
kind: issue
title: Verify the merge happened: re-read once after a delay, report a merge that did not land
parent: 042cxmtm4
needs: 042cxmtmg
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
After a forge merge call, re-read the PR; if it still reads open, wait about one second and read once more; if still not merged report exit 3 'merge not visible' (the forge call returned ok but nothing landed). The success line is printed only after the PR is `merged`. Because the ledger completes through `qew complete`, no automatic landing is performed here; the output carries the exact command to run (`qew complete ID`), and for epic PRs lists every covered item.

## Scenarios
- delayed visibility: first re-read open, second merged -> success. Prevents: false failure when the forge lags.
- merge that did not happen: both re-reads open -> exit 3. Prevents: telling the user work merged when it did not.
- epic PR merged: output lists each covered item and its `qew complete` command. Prevents: forgotten items.

## Reference coverage
Reference pr merge walk file: merge not yet visible re-read, merge that did not happen, landing failure reported with the command to rerun (landing itself is dropped: see dropped). 3 test functions.

## Qew today
Missing: `merge_pull_request` trusts the forge call and never re-reads.
