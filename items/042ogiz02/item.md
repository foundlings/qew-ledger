id: 042ogiz02
kind: issue
title: A pull request's covered items are frozen at open: pr check --add must extend them and pr sync --items must repair them
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-13T22:52:19Z
---
Santa: foundlings PRs 4428 and 4430 cannot merge because children created after pr open are not in record.items, so pr_gate.open_children refuses even with every box ticked. Fix: pr check --add also appends the item to the record; pr sync N --items re-derives items as recorded + covered_by(host) + items with a Progress box.
