id: 042cxmto3
kind: issue
title: A git pre-push / jj equivalent records evidence
parent: 042cxmto2
needs: 
labels: area:vcs-hook
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: prylwoyt
---
On push, a change citing a ledger ID must have its evidence recorded or the push is refused with the exact qew command; installed by `qew hook install`.
Scenarios:
- golden: cited id with evidence passes
- refusal: cited id without evidence blocks
- adversary: hook is bypassable only by removing it, which is itself visible in the diff
