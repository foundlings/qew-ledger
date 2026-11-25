id: 0453he13e
kind: issue
title: qew pr links, link and merge: a PR number exists on several targets and cannot be disambiguated
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

For Foundlings #8660, `qew pr links 8660 --target github-github.com-foundlings-foundlings-pr-8660`, `qew pr link 8660 --related 0450a8kg6 --target github-github.com-foundlings-foundlings-pr-8660`, and `qew pr merge 8660 --target github-github.com-foundlings-foundlings-pr-8660` refuse with `qew: pull request #8660 exists on several targets; pass --target`. The same forge PR is recorded as both hostless and item-linked records.

## Fix

Resolve a PR identity once per target and number. When hostless and item-linked records identify the same forge PR, use the item-linked record for item ownership and its declaration while preserving shared PR state; refuse only when records disagree on identity or state.

## Done when

Matching hostless and item-linked records let `qew pr links`, `qew pr link`, and `qew pr merge` select the PR with its exact target. Existing retarget, ready, and body operations continue to work. Conflicting identity, declaration, or state still fails closed.
