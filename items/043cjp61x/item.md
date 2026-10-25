id: 043cjp61x
kind: issue
title: jj ancestry lookup of a commit sha is a revset parse error and reads as not an ancestor
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-10-25T21:46:36Z
---
## Where

src/qew/code_vcs.py (_jj_change, is_ancestor, landing, _landing_many_jj)

## Problem

under jj 0.46.0 change_id(<hex sha>) is a parse error (change ids use only k-z), so is_ancestor returns False and qew pr merge A B C says no head contains the others

## Fix

emit change_id for k-z strings and commit_id for hex, never both; a failed revset raises exit 3 instead of reading as not an ancestor

## Done when

a hex head sha resolves through is_ancestor under jj, and a revset error is raised
