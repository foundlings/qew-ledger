id: 042de8kgd
kind: issue
title: Rewrite the security spec for read-side trust, and add a token-efficiency measurement
parent: 
needs: 
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T22:59:35Z
---
<!-- qew-duplicate -->

## Behaviour
docs/specs/security.md must state, for the ledger model: item titles, bodies, comments, actor names and branch names are untrusted data; routine reads (`ready`, `list`, `prime`, hook context) print bounded metadata only; bodies and comments appear only in explicit inspection (`show`, `triage`, `list --bodies`); prime and hook context re-validate approval locally, quote and byte-bound titles, withhold titles with suspicious Unicode, and state that data is not instructions; text findings are annotations pinned to a reviewed Unicode release; identifiers and search terms are never interpolated into shells, paths or forge queries; approval needs a human's quote. Add a measurement doc and a checked-in script that compares raw ledger bytes against compact `--json` output for ready, list, prime and show on a fixed fixture ledger, with exact UTF-8 byte sizes and a stdlib token proxy, failing when a command regresses past its recorded size.

## Scenarios
- drift: a test fails when security.md omits any of the named routine-read guarantees or when a documented guarantee lacks a walk. Prevents a spec that lies.
- regression: the measurement script run in `--check` mode fails when `ready --json` grows past the recorded bytes. Prevents silent token-cost regressions.

## Reference coverage
Reference security spec (explicit reads, Unicode annotations, execution rules) and reference measurement document with the generating script (ready -74%, list -64%, prime -53%, show -38% bytes).

## Qew today
Reduced. security.md is 12 lines and covers forge text, bounded HTTP, quoted approval; it has nothing on routine versus explicit reads, text findings, prime, or measured output size. No measurement doc.

---
042cxmtnk · approved · issue
Parent: #202
Blocked by: #223, #212, #213
