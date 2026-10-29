id: 0436rfyck
kind: issue
title: qew pr union builds the union of several pull request heads and pushes it as the lead's branch
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-23T00:37:13Z
discovered_from: 0436qot41
evidence: kxkrpoynkoyv squsvvsrmltt
---
## Goal

qew pr union N N... merges the heads of the given open pull requests into one commit (merge commits only, never a squash, every change id kept), refuses on a conflict naming the PR and files and pushing nothing, skips heads already contained, and pushes it forward-only as the first PR's branch, then verifies the remote has it. The lead's ownership rule applies (--other-author --reason). --dry-run builds and reports conflicts without pushing. Then qew pr merge N N... lands the batch. Born from rudolph hand-building the union with jj new, ancestry checks and a verified push.
