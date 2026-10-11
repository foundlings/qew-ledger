id: 042ifeuab
kind: issue
title: An open pull request cannot be retitled through qew: add qew pr sync N
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-11T10:56:34Z
---
Rudolph retitled item 042ge8e56 and could only close PR #4391 and open #4394. qew pr sync N sets the open PR's title from its item's title and records it in the ledger. The body is composed at open from --what/--why/--testing, with a checklist whose ticks live in the PR, so it is not regenerated. Also answer: an epic under an epic is refused by design (kinds nest epic > issue > task).
