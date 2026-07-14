---
description: NEM generation output for a DUID, station, fuel type, or region
argument-hint: "[entity] [period] e.g. Eraring last week"
---

The user wants NEM generation / output data from the SCADA Miner warehouse.

Request: $ARGUMENTS

Follow the SCADA Miner workflow:

1. Call `start_question` and reuse the returned `question_id` on every tool call.
2. Resolve the entity with `search_entities` — it returns ranked candidates
   (DUID code + station, station groupings, region/fuel aliases). Pick the
   candidate that fits the question; ignore weak matches for generic words.
3. If time-bounded, call `get_data_freshness` and clamp the range. Resolve undated
   phrases to the most recent past occurrence and restate the inferred year.
4. Call `list_capabilities` and prefer a matching generation/output capability via
   `run_capability`. Only fall back to `list_tables` / `search_columns` /
   `get_table_schema` + `execute_sql` if nothing fits — and read the schema
   `caveats` before composing SQL.
5. Chart with `build_chart` when a trend or breakdown helps. For multi-DUID or
   multi-fuel series, set `color` to that category rather than drawing one line
   through repeated timestamps.
6. Answer concisely with exact figures, units (MW vs MWh), and caveats.

Ask one clarifying question if the entity or period is ambiguous.
