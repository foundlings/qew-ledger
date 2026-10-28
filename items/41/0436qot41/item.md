id: 0436qot41
kind: issue
title: qew pr merge takes several pull requests and lands them as one batch
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-23T00:21:23Z
evidence: yzqymoytkwtz kunuulypqvpv
---
## Goal

qew pr merge A B C merges pull requests whose heads form one union (the lead's head contains every other head) through the merge gate once: every PR is gated, the lead is merged, each other PR is verified merged on the forge and its mirror record updated, and the hand-off lists each item. Agents reach for the verb they know, so no new flag or verb. Refuse when no head contains the rest, naming the jj/git recipe to build the union. Born from rudolph landing five PRs by hand with --integrator.
