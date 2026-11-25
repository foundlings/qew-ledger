id: 0453he13e
kind: issue
title: Deduplicate hostless and item-linked pull request records
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-25T03:29:26Z
---
## Where

qew PR record lookup and mutation commands

## Problem

The same forge PR number and target can be recorded once as a hostless PR and again as an item-linked mirror. qew pr retarget and qew pr ready count both records and refuse, even with the exact target selector, so a stacked PR cannot be retargeted or marked ready. This blocks Foundlings PR #8660.

## Fix

Resolve a PR identity once per target and number. When hostless and item-linked records identify the same forge PR, use the item-linked record for item ownership and its declaration while preserving the shared PR state; refuse only when the records disagree on identity or state.

## Done when

A fixture with matching hostless and item-linked PR records lets qew pr retarget, ready, and body operations select that PR with its target; a fixture with conflicting records still fails closed.
