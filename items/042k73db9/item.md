id: 042k73db9
kind: issue
title: Mirror targets come from the cwd repo's config even when QEW_LEDGER names another ledger; add mirror rehome
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-10-12T07:55:43Z
---
## Problem

QEW_LEDGER=A run from a checkout of repo B synced A's items into B's forge repository (foundlings items filed as foundlings/qew #484 and #485). Refuse the mismatch; add qew mirror rehome ITEM --from TARGET to close the stray issue and forget its record.

## Done when

A mismatched QEW_LEDGER is refused (exit 2) when the config has mirrors; qew mirror rehome closes the stray issue with a pointer, forgets the record, and the next sync files it in the configured target.
