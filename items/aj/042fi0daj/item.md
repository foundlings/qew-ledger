id: 042fi0daj
kind: issue
title: Stale baseline reported as a false divergence: forge=closed ledger=open for a completed item
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T00:05:38Z
evidence: yzmqozupoyzr ztuwlqowyvkm
---
Santa 2026-10-10: WP-AAV-06 (#3954), completed in the ledger, was reported state forge=closed ledger=open. The ledger value printed was the pull baseline (seen.open, written when the issue was still open: GitHub shows created 22:26, closed 22:48, divergence 23:17), not the ledger's own projection. Fix: the pull compares the forge with what the ledger projects (open unless completed or closed); when they agree the baseline is just refreshed, and a real divergence names the ledger's projected state.
