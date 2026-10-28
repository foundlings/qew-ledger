id: 04321194k
kind: issue
title: qew cannot resolve a landed change when the target bookmark is conflicted or the evidence change id is divergent
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-20T16:19:54Z
evidence: xpvplvxyzqmk ytqvurpxzntr
---
A jj checkout where main is a conflicted bookmark makes present(main) fail, and qew reports 'target main does not exist in this repo' (exit 3); a divergent evidence change id makes present(CHANGE) fail, so landing() calls the change unknown and is_ancestor() calls it not an ancestor. A temporary workspace in a busy repo hits both. Resolve the target through its bookmark sides when it is conflicted, and look changes up with change_id() as landing_many already does.
