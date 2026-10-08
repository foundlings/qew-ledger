id: 042cxmthi
kind: task
title: Inventory and walk coverage: qew list
parent: 042cxmthd
needs: 
labels: area:command-inventory status:Ready
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
Command inventory for `qew list`: list items.

Flags: --kind, --state, --label, --json.

End-to-end check (2026-10-08, scratch ledger + local forge fake, scripted run of every command): works, exit codes as documented.

Walk coverage today: 2 direct test invocation(s) of `qew list`; flags never exercised by any test: --state.

Done when: a golden scenario and the refusal/adversary scenarios for this command and each flag exist as named walks whose docstrings state the failure prevented, and the three documents (help, README, commands spec) agree.
