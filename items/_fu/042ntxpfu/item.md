id: 042ntxpfu
kind: issue
title: hook pre-tool: the jj git push decision snapshots the working copy and has no time bound
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-13T15:10:44Z
evidence: ymtrovwmwsmz ksskrtlxkvtt
---
Santa: pre-tool for jj git push exceeded the caller's 10 s cap under contention. Cause: vcs_check runs jj log without --ignore-working-copy (snapshot, working-copy lock) and without a timeout. Decision must be read-only and bounded, with a could-not-decide reason.
