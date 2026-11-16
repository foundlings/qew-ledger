id: 044mgni4o
kind: issue
title: pr ready and pr union refuse unticked checklist items, with an --allow-unticked override
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-16T16:46:03Z
evidence: qzqrttlrlluv wwmrqkvwupsn
---
## Problem

Agents run qew pr ready on PRs whose Progress checklist has unticked boxes; the failure surfaces only later at pr merge --check, at the integrator. Requested by Santa.

## Done when

pr ready N refuses (exit 2, nothing changed) while any box is unticked, naming each item with its fix commands; --allow-unticked --reason TEXT overrides and records it on the items and in the body; pr union refuses unticked boxes naming the source PR, same override; pr merge --check prints the same explanation; tests and docs
