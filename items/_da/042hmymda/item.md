id: 042hmymda
kind: issue
title: Manage pull request owner labels through qew
parent: 042cxmtm4
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-11T01:15:26Z
evidence: qunmlpzpquqv yqnrorulurpr
---
Provide a qew-owned command to add and remove pull request labels, preserve unrelated labels, enforce PR ownership, and verify the forge readback before recording success. Include command-level red/green fake-forge controls for label application, removal, foreign ownership and forge refusal. Required by Foundlings item 042hk5p6a: task label elf2 is recorded, but qew 6.8.0 pr open creates PR 4389 without labels, and pr help exposes no label operation. Evidence: gh pr view 4389 --json labels returns an empty labels array; cmd_pr.open_pull_request constructs PullRequestSpec without labels. Discovery is in the external foundlings ledger; its item ID cannot be a local discovered-from edge. Do not bypass the qew forge boundary.
