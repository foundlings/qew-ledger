id: 044wrjx9m
kind: issue
title: Reject unresolved evidence and add an audit-safe retraction
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-21T19:14:32Z
evidence: vnzusspo utmttwss ypwzzxwz
---
## Problem

The evidence command records syntactically valid change IDs that do not resolve in the configured code checkout, and an incorrect evidence event on open work cannot be retracted while preserving event history.

## Fix

Refuse unresolved evidence before writing, and let the item holder retract a cited change from an open item's effective evidence with a reason recorded in the ledger.

## Done when

Command tests prove unresolved IDs are refused without an event, resolvable changes are recorded, a cited ID can be retracted with an auditable reason, and uncited IDs or completed items are refused. README and command spec describe the interface.
