---
name: nem-market-analysis
description: >-
  Answer questions about Australia's National Electricity Market (NEM) / AEMO
  data — spot and FCAS prices, generation output, interconnector flows, network
  constraints, demand, bids, and generator revenue — using the SCADA Miner MCP
  server. Use whenever a question concerns NEM/AEMO electricity market data and
  the SCADA Miner tools are available. Guides Claude to resolve entities, prefer
  validated query capabilities, write safe read-only SQL only as a fallback, and
  return cited numbers with charts.
---

# NEM Market Analysis (SCADA Miner)

This skill helps you answer Australian National Electricity Market (NEM)
questions accurately using the **SCADA Miner** MCP server, which exposes a
ClickHouse warehouse of AEMO market data. Apply it whenever the user asks about
NEM/AEMO topics (prices, generation, FCAS, interconnectors, constraints, demand,
bids, revenue) and the SCADA Miner tools are connected.

## Key facts

- NEM time is **Australia/Brisbane (UTC+10, no daylight saving)**. Do date
  arithmetic in that zone.
- Regions are `NSW1`, `QLD1`, `SA1`, `TAS1`, `VIC1`.
- All warehouse access is **read-only**.

## Workflow

1. **Open a trace.** Call `start_question` with the user's question and pass the
   returned `question_id` on every subsequent tool call in the same answer turn.
2. **Resolve entities.** For each station / DUID / region / interconnector / fuel
   term, call `search_entities` and pick the candidate that fits the question's
   context. Ignore weak matches for generic English words (e.g. "demand",
   "power").
3. **Anchor time.** If the question is time-bounded, call `get_data_freshness`
   to clamp the range to available data. Resolve undated phrases (e.g. "March 3",
   "last week") to the most recent past occurrence and **always restate the
   inferred year** in your answer. Ask the user if a date is genuinely ambiguous.
4. **Prefer a capability.** Call `list_capabilities`; when one matches, use
   `run_capability` (with `execute: true`) — it returns pre-validated SQL, a
   chart, and often a deterministic answer. **Always prefer this over
   hand-written SQL.**
5. **Fall back carefully.** If no capability fits, locate the table with
   `list_tables` (by `domain`/`keywords`) or `search_columns` (by measure), then
   call `get_table_schema` and **read its `caveats`** (sign conventions,
   double-counting, partial coverage) before composing SQL. Execute with
   `execute_sql`. Add a time-column `WHERE` filter so ClickHouse can prune.
6. **Chart when it helps.** Use `build_chart` for trends, rankings, breakdowns,
   and comparisons. For multi-series data set `color` to the category instead of
   drawing one line through repeated timestamps. Use one chart per period for
   period-over-period comparisons, each titled with its period.
7. **Answer.** Concise, analyst style: cite exact numbers with units, state the
   resolved date range, and note caveats. Keep it brief unless detail is asked
   for.

## Pitfalls to avoid

- Do not explain a market mechanism from memory — call `get_concept` to ground
  it, or say you can't confirm.
- Do not hand-roll `max(SETTLEMENTDATE)` / full-table scans for freshness — use
  `get_data_freshness` or `list_tables` availability bounds.
- Do not query `raw_*` tables or `information_schema`/`system.*`; use the
  schema-discovery tools and the `consolidated.*` / `semantic.*` views.
- Stay in scope: only NEM / AEMO market data.
