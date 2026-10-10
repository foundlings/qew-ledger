id: 042etg25m
kind: issue
title: A large import fails to commit: every path is passed on the git command line
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-09T15:44:22Z
evidence: qqzrkmnourzt qoootmkswkmm
---
## Problem

qew create --from-file PLAN --import with 20110 items fails with 'ledger commit failed, the write was rolled back: cannot run git: Argument list too long'. ledger_repo.commit passes every touched path to git add, git commit and the jj fileset. The rollback also leaves the events directories behind, so qew check then reports 20111 problems (events belong to no item).

## Fix

Stage and commit paths through git's --pathspec-from-file with NUL separators on stdin (and the equivalent single fileset or chunked commits for jj); make the rollback remove every file the failed write created, events included.

## Done when

A walk imports more items than the OS argument limit allows in one command, commits once, and qew check passes; a walk whose commit is forced to fail leaves the ledger exactly as it was.
