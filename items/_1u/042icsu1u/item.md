id: 042icsu1u
kind: issue
title: Parsing a 22k-item ledger takes about 3 s of every read: parse events and items faster or not at all
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-11T10:02:54Z
evidence: mqtoltrw sxookuqy pvurzylu
---
After the snapshot cache (6.9.0) and the jj fix (6.9.1) the remaining cost of a read on foundlings is parsing 142k events (about 2.3 s) and 22.5k items (about 1 s), plus stat validation. Options measured or noted: valid_actor and per-event validation overhead, lazy parsing (fold needs state only), caching the folded state per item in snapshot.db (skips event parse for unchanged items), never pickle a parsed object cache (a swapped file would run code). Acceptance: warm read of the foundlings copy under 2 s; no change in what any command prints.
