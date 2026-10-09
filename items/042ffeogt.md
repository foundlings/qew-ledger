id: 042ffeogt
kind: issue
title: qew attach, detach and show listing; qew check validates references
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:12:43Z
---
qew attach ID PATH [--as NAME] (file or directory, recursive), qew detach ID NAME, qew export ID DIR (materialise the named tree), qew show lists attachments with name, size, hash. Body references (relative links attachment:NAME) are validated by qew check: dangling reference, missing blob, hash mismatch, over-limit file fail loudly. One ledger commit per command (existing write path). Help, README, commands.md updated together (test_help_walk).
