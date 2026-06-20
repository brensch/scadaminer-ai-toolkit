---
description: List the validated NEM question shapes ScadaMiner can answer
---

Show the user what the ScadaMiner warehouse can answer out of the box.

1. Call `list_capabilities` to retrieve the registered, validated SQL builders
   (prices, demand, generation output, revenue, constraints, FCAS,
   interconnectors, and more).
2. Group them by domain and present a short, readable menu — capability name and
   a one-line description of the question it answers.
3. Invite the user to pick one or phrase their own question; note that anything
   not covered by a capability can still be answered with custom SQL.

Do not run any capability yet — this is a discovery step.
