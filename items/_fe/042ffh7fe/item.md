id: 042ffh7fe
kind: issue
title: Comments mirror both ways with GitHub issue comments
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:14:12Z
evidence: mwqvloktqqqk vzturppyvmno
---
Pull already imports forge comments as commented events. Add: push ledger comments to the forge (idempotent: the mirror record keeps comment id -> forge comment id; under the existing pacing, concurrency and authority rules; a comment body carries a marker so a rerun or another machine adopts instead of duplicating), edits and deletes both ways (ledger edit event updates the forge comment, forge edit imports as comment_edited with provenance forge; a delete on either side hides the comment on the other with the history kept), threading degrades to a quoted reply line on GitHub (issue comments have no parents), attachments referenced in a comment appear as links like the issue body section. Define the both-sides-edited case: last writer by time wins and the loser is kept as a divergence for qew conflicts. Forge text stays untrusted data.
