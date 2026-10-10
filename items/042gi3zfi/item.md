id: 042gi3zfi
kind: issue
title: Recover evidence for completed items: qew evidence --manifest also fills the header of historical completions
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T12:02:19Z
---
Santa wants to recover real change ids from foundlings' phase docs AFTER the schema 4 migration (items completed as historical). Today evidence needs an approved or claimed item. Allow rows for completed items whose header says evidence_absent: historical (or has evidence): the evidence event is recorded and the header gets the ids, replacing the historical absence. Other absences (no-code, children, superseded-by) are refused: they are stated facts.
