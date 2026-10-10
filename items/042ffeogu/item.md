id: 042ffeogu
kind: issue
title: Mirror behaviour for attachments: links at the synced commit, never silent uploads
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:12:43Z
evidence: ltwtqnmnzuro mpnrmryqoxxq
---
A generated Attachments section in the forge issue body: names with links to the ledger repository path at the synced commit (GitHub blob URL of items/ID/attachments/HASH.EXT), sizes and hashes; qew never uploads binaries into issue bodies or the forge asset store. Forges without a web view degrade to a plain list. Pull ignores edits to the generated section (forge text is untrusted data). Walk against the GitHub fake: section appears, changes with attach/detach, a forge-side edit of it is not imported.
