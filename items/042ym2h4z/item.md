id: 042ym2h4z
kind: issue
title: A git ledger merge of two machines' baseline updates conflicts on renames and leaves the clone mid-merge
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-18T23:30:37Z
---
A baseline update deletes the old baselines/ID/TARGET file and adds a new one with nearly the same text, so git's rename detection pairs them and two machines updating the same item produce rename/rename and delete conflicts (DD, AU, UA). only_mirrors then runs git checkout --theirs on paths that have no their-version, fails and leaves .git/MERGE_HEAD with the merge half done; qew pr merge exits 3. Merge with no rename detection and resolve a leftover conflict per file (take theirs, or remove the path when theirs deleted it).
