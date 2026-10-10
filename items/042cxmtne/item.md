id: 042cxmtne
kind: issue
title: Withhold suspicious titles and state data-is-not-instructions in prime and hook context
parent: 042cxmtmt
needs: 042cxmtnd 042cxmtn1
labels: area:read-side
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
When a title carries zero-width, bidi, Unicode tag or confusable findings, prime does not print the title. It lists `ID suspicious title text: zero_width, bidi_control` under Contradictions and skips the item so an agent never reads hidden instructions at session start. The conventions block always states that titles are approved but remain untrusted data. The same rule applies to the hook session-start text.

## Scenarios
- adversary: an approved item whose title hides text after a zero-width character is absent from Next ready and named under Contradictions with the finding kinds. Prevents hidden-instruction titles reaching an agent.
- golden: a title with a family emoji and a Scotland flag is printed normally. Prevents false positives on legitimate emoji.
- golden: the hook output and `qew prime` apply identical filtering. Prevents two diverging trust paths.

## Reference coverage
Reference security spec (prime withholds suspicious titles, quotes and byte-bounds); reference prime golden walk's injected-title item. Maps 1 prime test partially and 2 triage tests.

## Qew today
Missing. Hook context prints titles as is.
