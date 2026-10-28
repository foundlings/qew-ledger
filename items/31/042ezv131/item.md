id: 042ezv131
kind: issue
title: qew sync lists every forge issue twice per create, so a large first sync is quadratic
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T17:55:01Z
evidence: vqwlqull zyvvqtot
---
Observed 2026-10-09: foundlings real sync (1837 creates, GitHub) makes about 2 issues per minute, process at 0.4% CPU waiting on HTTP, no sleep or throttle in the create path. Cause: sync._find_or_create runs forge.find_issue (full paged listing of ALL issues, per_page=100) before each create when the sync is not scoped (recent=False) and again after the create for the duplicate guard. Cost per item grows with the repo: ~2 full listings per create, so ~N/100*2 requests each. Fix direction: one marker index per target built from a single listing at the start of a full sync, updated as creates land; keep the interrupted-create adoption and the lowest-number duplicate rule; add a walk counting forge requests for a 200-item first sync (linear, not quadratic).
