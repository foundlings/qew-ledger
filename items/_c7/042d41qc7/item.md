id: 042d41qc7
kind: issue
title: Merged branches are deleted automatically: qew pr merge removes its head branch; qew branch prune clears the backlog
parent: 
needs: 
labels: area:branches
owner: 
priority: 1
created: 2026-10-08T19:31:25Z
evidence: souswoppxxto
---
Owner report: merged branches are not cleaned up, and the remotes have piled up branches (foundlings alone has 440).

Behaviour: (1) `qew pr merge` deletes the pull request's head branch on the forge after a successful merge, never the base, the target branch or a branch another open pull request uses; (2) `qew branch prune [--target T] [--base BRANCH] [--dry-run]` lists the forge's branches and deletes those whose tip is already contained in the base and that no open pull request uses; the default branch and the base are never touched; dry-run is the default output shape and deletion needs no extra flag but prints every name it deletes; (3) forge interface gains list_branches, branch_is_merged, delete_branch (GitHub and Forgejo/Gitea; GitLab stays unsupported).

Scenarios: golden: merge removes the head branch; refusal: a head shared by another open pull request survives; golden: prune deletes only merged, unused branches; adversary: base and default branch are never deleted even when 'merged'; dry-run deletes nothing; forge down leaves everything.
