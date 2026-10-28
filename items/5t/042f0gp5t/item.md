id: 042f0gp5t
kind: issue
title: Sync must keep the forge close reason: a completed issue pulled stays completed, duplicates close as duplicate, and wrongly not-planned imports are repaired
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T18:07:39Z
evidence: stommmyt klwrzlmn
---
Owner report 2026-10-09: sync closes many issues as 'not planned' (foundlings/foundlings 30 issues, qew itself). Cause: forge_pull._import_issue and ledger_import._restore_item record every closed forge issue as closed/not_planned ignoring state_reason; the next push rewrites GitHub to not_planned. sync_plan._CLOSE_REASON and the duplicate guards in sync.py/forge_pull.py also send not_planned for duplicate/superseded. Fix: (a) parse state_reason on RemoteIssue; GitHub completed or no reason -> ledger completed (forge-import), not_planned -> closed not_planned, duplicate -> closed duplicate; (b) a repair command that re-reads the first closed event's state_reason from the forge timeline for forge-import closed/not_planned items and corrects ledger (reopened + completed, append-only) and forge; (c) run it on qew's own ledger and relay for foundlings; (d) walks: completed stays completed across a sync round trip, duplicates close as duplicate; superseded maps to duplicate (documented).
