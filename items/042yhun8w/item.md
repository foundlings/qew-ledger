id: 042yhun8w
kind: issue
title: A read that races a writer reports the new item as an orphan and refuses with 'ledger is not readable'
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-18T22:24:47Z
evidence: yzrkonuwxxuk xlnzxuunuxum
---
Seen on foundlings-ledger while elf3 filed items in a series: qew show failed with 'the ledger is not readable: events/X: belongs to no item (and 1 more)', each time naming the newest id, though the files are all there afterwards. The snapshot lists item directories at one moment and the orphan check lists the events, mirrors and items directories at a later one, so an item written in between is reported as an orphan. read_snapshot must take a fresh look before refusing, so a transient partial state is not an error.
