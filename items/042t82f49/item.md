id: 042t82f49
kind: issue
title: Pull imports claim and release arbitration comments as ordinary comments
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-16T07:32:15Z
---
comment_sync.pull turns every forge comment into a ledger comment, including the qew:claim and qew:release markers qew posts itself; they are arbitration, not discussion, and clutter qew show. Skip them on pull. Santa asked.
