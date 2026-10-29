id: 042epukcn
kind: issue
title: A ledger imported by an older importer is refused whole: completions with empty original_ids
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-09T14:30:35Z
---
## Problem

The foundlings-ledger holds 4304 completed events with provenance import and original_ids empty (written by an early importer). The finished qew refuses every command on that ledger: an import completion must list the original_ids it stands for.

## Fix

Give qew a repair for legacy import completions (fill original_ids from the event source, or accept empty ones as unverified with a count in qew check), so an already-imported ledger opens without a re-import.

## Done when

A walk with an empty-original_ids import completion opens, qew check reports it as imported without evidence, and nothing is rewritten unless the repair command runs.
