id: 042yfn03x
kind: issue
title: A jj ledger write fails when the working copy sits beside main: commit refuses to move the bookmark sideways
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-18T21:39:30Z
evidence: pyylyumtwknn tsvlvxvrtwlq
---
Seen on foundlings-ledger after the schema 7 sync: qew start failed with 'ledger commit failed, the write was rolled back: Refusing to move bookmark backwards or sideways: main'. main sat on a merge commit while the working copy's ancestry was a side chain of about ten qew commits (evidence, pr-open) that main did not contain, so commit()'s bookmark set main -r @- was not a forward move, and every later write added to the chain and rolled back. commit() must merge the chain into main (jj new main @-) instead of refusing, the way fetch-merge already merges diverged sides.
