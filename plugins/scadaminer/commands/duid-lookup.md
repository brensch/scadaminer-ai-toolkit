---
description: Resolve a NEM station or DUID and show its key facts
argument-hint: "[station or DUID] e.g. Hornsdale or HPRG1"
---

The user wants to identify a NEM facility in the ScadaMiner warehouse.

Lookup: $ARGUMENTS

1. Call `start_question`, then `search_entities` with the term. Present the ranked
   candidates with their similarity scores and context: DUID code, station name,
   region, and fuel type.
2. If one clear match exists, summarise its facts (DUID, station, region, fuel,
   registered capacity). Use `get_concept` or a `run_capability` registration
   lookup if available to enrich the answer.
3. If several plausible candidates exist, list them and ask which the user means.

Keep it factual and brief — this is an identity/resolution step, not an analysis.
