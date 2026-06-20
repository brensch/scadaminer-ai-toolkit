---
description: NEM spot or FCAS price for a region over a time period
argument-hint: "[region] [period] e.g. NSW1 last 7 days"
---

The user wants NEM price data from the ScadaMiner warehouse.

Request: $ARGUMENTS

Follow the ScadaMiner workflow:

1. Call `start_question` with the user's request to open a trace, and pass the
   returned `question_id` on every later tool call this turn.
2. Resolve any region / interconnector / station term with `search_entities`.
   NEM regions are `NSW1`, `QLD1`, `SA1`, `TAS1`, `VIC1`.
3. Call `get_data_freshness` if the request is time-bounded, and clamp the range
   to available data. NEM time is Australia/Brisbane (UTC+10, no DST). Resolve
   any undated phrase to the most recent past occurrence and restate the year.
4. Call `list_capabilities` and prefer a matching price capability via
   `run_capability` — it returns validated SQL, a chart, and a deterministic
   answer. Only hand-write SQL with `execute_sql` if no capability fits.
5. Build a chart with `build_chart` (or use the capability's `chart_figure`).
6. Answer concisely with exact numbers, the resolved date range, and any caveats.

If the region or period is missing or ambiguous, ask one clarifying question
before querying.
