id: 042d30wf4
kind: issue
title: qew never derives an identity from the OS login: actors come from the configured git/jj user
parent: 
needs: 
labels: area:identity
owner: 
priority: 0
created: 2026-10-08T19:10:31Z
evidence: qqsvopms
---
The owner's OS login leaked into the ledgers as event actors, claim owners and commit messages (`qew: start ID by <login>`). The identity must be the configured VCS user (git config user.name, else jj user.name), never $USER.

Behaviour: actor() = QEW_ACTOR, else `git config user.name` in the code repo, else the ledger's, else jj `user.name`; never the OS login; an unresolvable identity refuses writes naming the config to set. Existing events keep their text (history rewrite is a separate tool).

Scenarios: golden: no QEW_ACTOR and USER=someone-else writes the configured name; refusal: no configured identity refuses the write; adversary: a name with whitespace or control characters is refused (existing safe-token rule).
