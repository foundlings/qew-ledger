id: 042eubbf0
kind: issue
title: A needs chain over 30 edges is a warning, not a failing check
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T16:02:01Z
evidence: xyxuplnlvnyk nmpvuktluyzt
---
## Problem

qew check fails a ledger whose longest needs chain exceeds 20 edges; the foundlings corpus has real chains of 22 and 24 and the check cannot pass.

## Fix

Raise the limit to 30 and report a longer chain as a non-fatal warning line beside the depth count, exit 0.

## Done when

A walk with a 31-edge chain gets a warning and exit 0; a 25-edge chain gets no finding.
