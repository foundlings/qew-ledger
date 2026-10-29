id: 042cxmthf
kind: task
title: Inventory and walk coverage: qew create
parent: 042cxmthd
needs: 
labels: area:command-inventory
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: qywskxnzlumw
---
Command inventory for `qew create`: file an item (a draft unless --quote releases it).

Flags: --kind, --title, --parent, --needs, --label, --priority, --body, --body-file, --quote, --from-file, --import.

End-to-end check (2026-10-08, scratch ledger + local forge fake, scripted run of every command): works, exit codes as documented.

Walk coverage today: 8 direct test invocation(s) of `qew create`; flags never exercised by any test: --body-file.

Done when: a golden scenario and the refusal/adversary scenarios for this command and each flag exist as named walks whose docstrings state the failure prevented, and the three documents (help, README, commands spec) agree.
