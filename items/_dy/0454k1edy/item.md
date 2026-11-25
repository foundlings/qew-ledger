id: 0454k1edy
kind: issue
title: Adopt an existing no-item PR by number
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-25T16:17:54Z
---
## Problem

`qew pr open --no-item ... --adopt-legacy N --reason ...` ignores the adoption flag, then forge creation rejects the existing head. This leaves an unrecorded legacy PR impossible to adopt.

## Fix

Validate the explicitly named open unrecorded PR against the requested head, base and mirror, update its no-item declaration/body, and record the existing number without creating a second PR.

## Done when

Command walks prove adoption preserves the PR number/head, records its no-item declaration and body, and refuses mismatched, closed, or already-recorded PRs.
