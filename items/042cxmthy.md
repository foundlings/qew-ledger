id: 042cxmthy
kind: task
title: Inventory and walk coverage: qew hook remove
parent: 042cxmthd
needs: 
labels: area:command-inventory status:Ready
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
Command inventory for `qew hook remove`: remove Qew's agent hook entries.

Flags: --claude, --codex, --cursor, --opencode.

End-to-end check (2026-10-08, scratch ledger + local forge fake, scripted run of every command): works, exit codes as documented.

Walk coverage today: 3 direct test invocation(s) of `qew hook remove`; flags never exercised by any test: none.

Done when: a golden scenario and the refusal/adversary scenarios for this command and each flag exist as named walks whose docstrings state the failure prevented, and the three documents (help, README, commands spec) agree.
