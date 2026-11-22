id: 044yb60cz
kind: issue
title: qew pr retarget N --base BRANCH: move a pull request's base on the forge and record it
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-11-22T13:49:20Z
---
## Where

src/qew/cmd_pr.py, pr_retarget.py, forge backends

## Problem

Stacked lane pull requests (foundlings #8269, #8280) are based on another branch, so they cannot join a union with main-based ones ('do not share one base branch'), and the hook forbids gh pr edit. qew has no way to change a pull request's base.

## Fix

qew pr retarget N --base BRANCH rewrites the forge base, records it on the pull request's ledger record, and refuses when the head does not contain the merge base of the old and new base; no-op when already based there. Optionally union offers it for stacked members whose base is in the union.

## Done when

A walk shows a stacked PR retargeted to main (forge and ledger agree), a head without that merge base refused with nothing changed, a finished PR refused, and a rerun a no-op.
