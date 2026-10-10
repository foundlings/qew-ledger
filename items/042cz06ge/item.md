id: 042cz06ge
kind: issue
title: qew pr ready must record draft:false in the pr mirror (and run in a ledger session)
parent: 
needs: 
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:48:26Z
---
Found by the drafts lane: draft revert refuses approved work whose pr mirror is not recorded as draft (draft key is not true). qew pr open now records draft; qew pr ready flips the forge flag but leaves the mirror saying draft true, and pr ready is not a ledger-writing verb in replication.verb_for, so a mirror rewrite would be uncommitted. Record draft false on ready inside a session verb.
