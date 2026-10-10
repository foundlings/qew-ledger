id: 042cxmthg
kind: task
title: Inventory and walk coverage: qew set
parent: 042cxmthd
needs: 
labels: area:command-inventory
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: qywskxnzlumw
---
Command inventory for `qew set`: change an item's header fields.

Flags: --title, --parent, --needs, --labels, --priority, --body.

End-to-end check (2026-10-08, scratch ledger + local forge fake, scripted run of every command): works, exit codes as documented.

Walk coverage today: 5 direct test invocation(s) of `qew set`; flags never exercised by any test: --labels.

Done when: a golden scenario and the refusal/adversary scenarios for this command and each flag exist as named walks whose docstrings state the failure prevented, and the three documents (help, README, commands spec) agree.
