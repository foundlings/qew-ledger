id: 042cxmti4
kind: task
title: Inventory and walk coverage: qew pr open
parent: 042cxmthd
needs: 
labels: area:command-inventory
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
Command inventory for `qew pr open`: open a draft pull request for an item.

Flags: --target, --head, --base, --ready.

End-to-end check (2026-10-08, scratch ledger + local forge fake, scripted run of every command): works, exit codes as documented.

Walk coverage today: 1 direct test invocation(s) of `qew pr open`; flags never exercised by any test: --base, --ready.

Done when: a golden scenario and the refusal/adversary scenarios for this command and each flag exist as named walks whose docstrings state the failure prevented, and the three documents (help, README, commands spec) agree.
