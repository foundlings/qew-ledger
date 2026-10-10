id: 042f4st7i
kind: issue
title: A secondary-limit 403 backs off longer than 60 seconds and prints the realistic resume time
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T19:35:48Z
evidence: lupmklzr pspozous
---
GitHub's 'secondary rate limit ... temporarily blocked from content creation' blocks last several minutes; qew said retry after 60s. Honour Retry-After when given; with none, back off several minutes (escalating on repeats) and print the time at which a rerun is likely to work. Walk: fake answers 403 secondary-limit text without Retry-After; assert the longer wait is recorded and printed.
