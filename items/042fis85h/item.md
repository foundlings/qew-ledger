id: 042fis85h
kind: issue
title: qew next-id and strict letter ids: ask qew for the next free id, mnemonic epic ids out
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T00:21:18Z
---
Owner 2026-10-10: 'I told you to make a command for qew to get the next free id'; letters are strict order, mnemonic names out: 'after ZZZ comes AAAA'. (1) qew next-id [--kind K] [--count N] prints the next free ids of the kind's id_mode. (2) The letters successor continues the real sequence and ignores far-off outliers (an id more than 676 ranks past the end of the main run, like PI/PID/PIE in foundlings after ADF), so ADG not PIF. (3) A plan that names an epic id in a letters kind (outside --import) must give exactly the next letter, else it is refused naming it. Rename of existing outliers (PIE -> ADG) and the new default (epic letters, issue and task base35-time) follow as their own items.
