id: 042gr3xbn
kind: issue
title: Imported completions with evidence events get their evidence header; repair-evidence rebuilds missing headers
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T14:45:37Z
---
Santa (foundlings-ledger 042gqb12z, elf5): qew create --from-file --import with COMPLETED entries carrying evidence events wrote no evidence header (154 items red in qew check), and qew evidence --manifest reported them unchanged because its test looks only at events. Fix: (1) the import path builds the header from the entry's evidence (resolved ids -> evidence; none -> evidence_absent historical with the import reason); (2) qew repair-evidence [--dry-run] rebuilds a missing header from the events, validating they landed; (3) evidence --manifest treats a completed item whose header lacks the ids as changed (header only, no duplicate event).
