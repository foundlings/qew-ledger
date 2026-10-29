id: 0436f2m7b
kind: issue
title: A ledger push or fetch timeout reads as unreachable, defaults to 5s, and unpushed work grows silently
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-22T20:44:51Z
discovered_from: 04368mzbn
evidence: nqqsoryuylzq qyotktmslnry
---
## Problem

With [replication] timeout_s at its 5s default a slow link (fetch 15s, push 8s) times out and qew reports remote=offline; every write stays local, the warning does not say how many commits are unpushed or name the setting, status shows no reason, and a PR record never reached the integrator (wolf reached unpushed=126)

## Done when

a timeout says it timed out after Ns and names [replication] timeout_s; the warning counts the unpushed commits and says other machines cannot see them; qew status shows the last remote error; the default timeout_s is 30
