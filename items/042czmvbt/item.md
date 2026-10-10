id: 042czmvbt
kind: issue
title: A carriage return in a title corrupts the item file (read back as a line break)
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-08T18:01:05Z
---
qew create --title $'a\rb' passes the one-line check (only a newline is refused) but the file is read with universal newlines, so every later read fails with malformed header line. Refuse CR (and other line separators) in titles at create and set, and make check report it.
