# scadaminer (Claude Code plugin)

Adds the [SCADA Miner](https://chat.scadaminer.com) NEM data connector to Claude
Code, plus NEM slash commands and an analyst subagent.

## Install

```
/plugin marketplace add brensch/scadaminer-ai-toolkit
/plugin install scadaminer@scadaminer
```

Sign in (OAuth) when Claude first uses a SCADA Miner tool.

## Contents

- **MCP server** `scadaminer` → `https://chat.scadaminer.com/mcp` (tools:
  `search_entities`, `get_data_freshness`, `list_tables`, `search_columns`,
  `get_table_schema`, `execute_sql`, `list_capabilities`, `run_capability`,
  `build_chart`, `get_concept`, `start_question`).
- **Commands:** `/scadaminer:nem-price`, `/scadaminer:nem-generation`,
  `/scadaminer:duid-lookup`, `/scadaminer:nem-capabilities`.
- **Subagent:** `nem-analyst`.

## Connector only

If you just want the data connection without the commands/subagent:

```
claude mcp add --transport http scadaminer https://chat.scadaminer.com/mcp
```
