id: 042ffh7bj
kind: issue
title: Comments as first-class records: stable ids, reply-to, edit and delete events, attachment references
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:14:12Z
---
State today: qew comment appends a commented event (text, author, optional key) and the pull imports forge comments with remote_ref. Missing: a stable comment id (the event id is the comment id), reply_to another comment, comment_edited and comment_deleted events (history kept, last event by id wins, so two machines never write the same file: conflict-free like attachments), references to attachments by named path (validated by qew check), qew comment --reply-to ID, qew comment edit ID and delete ID (author or a human only), qew show lists the threaded comments with author and time. Specified in docs/specs/ledger.md first.
