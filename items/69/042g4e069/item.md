id: 042g4e069
kind: issue
title: Bulk completion: qew complete --manifest FILE with a human's quote, one commit, no claim needed
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T07:22:20Z
evidence: vlktmmwxvrok xnyzqvoqpkln
---
Requested by Santa for foundlings (owner order relayed: items outside open phases must become DONE, #570/measure-board.py; 4,208 items; 710 mirrored). Today qew complete is one item per call, needs a claim and evidence.

Design (needs owner go): qew complete --manifest FILE --quote "Name: 'their words'" [--dry-run]. FILE is JSON Lines {item, reason?}. The quote is required (a human's words, same rule as draft approve) because this completes work nobody claimed or evidenced: it is recorded on each event as the authority, plus the per-row reason. Every row is checked before the first write (unknown item, draft, already closed-not-planned, duplicate row, malformed JSON all refuse the whole manifest, naming the row); an item already completed is unchanged (idempotent rerun). Works on approved unclaimed items without a claim; an item claimed by ANOTHER login is refused unless it is in the manifest with force (not in v1: refuse). Events: approved items get a completed event with provenance bulk-complete, the quote and reason; drafts are refused (release them first). One ledger commit for all rows (like attach/comment manifests). A later sync closes the mirrored issues as completed (not not_planned) through the existing completed path. Walks: golden (3 items, one commit, states completed), one bad row refuses all and writes nothing, rerun unchanged, foreign claim refused, quote required, sync closes the GitHub issue as completed.
