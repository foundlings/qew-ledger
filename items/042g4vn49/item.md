id: 042g4vn49
kind: issue
title: Agents file work straight into the queue: qew create is Backlog or Ready, drafts only on a human's request
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T07:32:02Z
evidence: vptznmsnntrm ornkxwnxqtmw
---
Owner order relayed by Santa (verbatim): 'when it finds items they are in the normal queue. draft is for humans when I request a draft. omfg. everything else is either backlog or ready'. Today every qew create by an agent is a draft that only a human's quote releases (CLAUDE.md: 'Work that is not human-approved is a draft').

Change: qew create (also --from-file, plan files, bulk paths) writes work approved by default: Backlog when it has unmet needs, Ready otherwise; --draft is for drafts a human asked for. The creator stays recorded (author + discovered_from, and the approved event carries provenance agent-filed instead of a human quote). Keep qew draft approve --quote for human-requested drafts. Update the docs, CLAUDE.md/AGENTS text, hook text and skill text that say everything an agent files is a draft or never self-approve. Open design point for the owner: this removes the human gate on what enters the ready queue (an agent can now file work other agents will start); the claim, evidence and complete gates are unchanged. Walks: create lands ready, create with needs lands backlog, --draft stays a draft, creator recorded, plan files and from-file follow, hooks text updated.
