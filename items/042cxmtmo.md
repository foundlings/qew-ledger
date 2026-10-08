id: 042cxmtmo
kind: issue
title: Decide merge-to-complete hand-off: after merge print the evidence and complete steps per item
parent: 042cxmtm4
needs: 042cxmtmh
labels: area:pull-requests
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
The reference lands (closes) issues automatically after merge. In qew completion needs recorded evidence and `qew complete`; this issue only requires that a merge outcome is actionable: the output prints, per covered item, `qew evidence ID --change CHANGE` and `qew complete ID` and names the merge commit; a merge whose item cannot yet be completed (open children) says why. No auto-completion.

## Scenarios
- merge of single-item PR prints the evidence and complete commands. Prevents: merged-but-never-completed work.
- item with open child tasks: hint names the blocking children.

## Reference coverage
Replaces the reference landing (golden walk lands, landing failure rerun hint) with the ledger equivalent. 1 test function mapped here.

## Qew today
Reduced: the success line says only 'record evidence and run `qew complete ID`'.
