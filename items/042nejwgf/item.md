id: 042nejwgf
kind: issue
title: Link a pull request to the items it delivers on the forge (Development sidebar) without losing qew's completion rule
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-13T10:17:26Z
---
## Problem

qew pr open writes no closing keyword, so no pull request shows in the Development sidebar of the issues it implements; the only GitHub link is a closing reference (body keyword or addCloseIssueReferences), which closes the issue on merge. No repo-level API option stops that.

## Done when

pr open/check link each Progress item; a forge closure caused by a linked PR is expected, not a divergence, and the item is completed with evidence; parents get a non-closing Part of line; a repair command backfills open PRs.
