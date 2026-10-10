id: 042ffeogv
kind: issue
title: Migration: the attachment layout is additive; schema_version gate instead of a rewrite
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:12:43Z
evidence: srupwkortppp kzmnmnsmmtrv
---
Because attachments live in items/ID/ beside items/ID.md and are named by new events, existing ledgers (qew's own and foundlings) stay valid byte for byte: there is nothing to rewrite. What is needed: qew init and a first attach set ledger schema_version to 2 and older binaries must refuse a ledger that uses attachments loudly (unknown event type already fails validation; make the message name the needed qew version), qew check green before and after. If the owner still wants an explicit command, qew migrate-layout [--dry-run] would only report and bump schema_version in one commit, refusing while another login holds a claim. Decide with the owner whether the command is worth having. Both ledgers: qew's own first, foundlings after Santa says the sync is done.
