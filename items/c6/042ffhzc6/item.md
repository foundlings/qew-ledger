id: 042ffhzc6
kind: issue
title: What GitHub issues carry that the ledger cannot hold yet: analysis and recommendation
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:14:39Z
---
What a GitHub issue carries, what the ledger holds, and my recommendation (the owner decides which to build).

HELD today: title, body, state with reason (completed, not planned, duplicate), labels (user labels both ways; kind, priority, status managed), one assignee (owner, via the mirror assignees map), milestones (epics become milestones), dependencies (needs become blocked-by links), board column and priority (project cards), linked pull requests (pr mirror records, qew pr), comments (pull only: forge comments become commented events; push is missing).

NOT HELD, with a recommendation:
1. Comments push, edit, delete, replies: BUILD (approved, children of the attachments epic).
2. Attachments and images in the body or comments: BUILD (approved). GitHub-hosted user-attachments URLs in imported text stay as text links; importing the bytes needs the owner's explicit option.
3. Sub-issues (GitHub native parent/child): RECOMMEND BUILD small: map the ledger parent to the sub-issue relation so the forge shows the same tree; the ledger stays the truth.
4. Several assignees: RECOMMEND SKIP: the ledger has one owner by design (one claim); extra assignees would contradict claims.
5. Reactions: RECOMMEND SKIP: noise; a reaction is not work state; mention in the mirror docs that they are not imported.
6. Issue types and custom project fields beyond Status and Priority: RECOMMEND LATER: only if the owner uses them; a per-mirror field map option would do it.
7. Timeline events (renamed, labeled, assigned, cross-references, mentions): RECOMMEND SKIP as records: the ledger events are the history; for IMPORT only, closed/reopened with reasons are already read. Optional import-time summary event if the owner wants provenance.
8. Issue body edit history: SKIP (the forge keeps it; the ledger keeps its own field events).
9. Locked, pinned, subscribers, participants: SKIP.
10. Cross-repository issue references: RECOMMEND LATER: store as untrusted text links only.
11. Pull request reviews and review comments: out of scope for items; qew pr covers merge gates. Could import as comments on the pr record if the owner wants them: DECIDE.
Next step: the owner picks from 3, 6, 10 and 11; everything else stays as recommended.
