id: 042cxmto0
kind: issue
title: Real-world test drive against foundlings/qew-ledger and the GitHub project
parent: 042cxmtnm
needs: 042cxmtnz 042cxmtnw
labels: area:replication
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
---
Clone the ledger into 2-3 scratch checkouts, run qew as different agents (claim, evidence, complete, comment, create), push, show convergence; make one change directly on GitHub via the API and show it imported as an event or divergence. Every finding becomes an issue and a scenario test; record what converged and what did not.
Scenarios (each a named walk whose docstring states the failure it prevents):
- golden: the test drive report is recorded as a comment on this issue
