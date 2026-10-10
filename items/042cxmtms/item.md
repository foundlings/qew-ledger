id: 042cxmtms
kind: issue
title: Keep `qew pr` help, README and commands.md in agreement for every new subcommand and flag
parent: 042cxmtm4
needs: 042cxmtmc 042cxmtmk 042cxmtmm 042cxmtmf 042cxmtm7
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Each subcommand/flag added by the issues above has a `--help` line, a README entry and a `docs/specs/commands.md` entry, and `pr check` joins the epilog group. The forges.md spec lists the new `Forge` capabilities and their Unsupported cases. The existing help walk is the gate.

## Scenarios
- help walk fails when a new flag has no help line, README or spec mention. Prevents: undocumented surface.

## Reference coverage
Repo rule on three-place agreement; no reference test (the reference help walk is another area).

## Qew today
commands.md describes `pr open|ready|merge` in three lines; README lists the three subcommands only.
