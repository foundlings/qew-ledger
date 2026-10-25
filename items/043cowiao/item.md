id: 043cowiao
kind: issue
title: Batch merge ignores --other-author --reason for a follower claimed by another actor
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-10-25T23:12:33Z
---
## Where

src/qew/pr_batch.py (_heads, merge_batch)

## Problem

_heads and the follower loop call load with an empty reason, so require_owner refuses any follower whose items another actor claimed although --other-author --reason was given; each pull request alone passes

## Fix

thread the merge reason (when --other-author is set) into every load the batch makes

## Done when

a batch with a foreign-claimed follower merges under --other-author --reason and is still refused without it
