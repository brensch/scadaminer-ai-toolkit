# ScadaMiner AI Toolkit

Connect Claude to **[ScadaMiner](https://chat.scadaminer.com)** — an AI-ready data
warehouse for Australia's National Electricity Market (NEM). Ask natural-language
questions about AEMO dispatch data: spot prices, generation output, FCAS markets,
interconnector flows, constraints, bids, and more. Claude turns them into safe,
read-only SQL against the warehouse and answers with numbers and charts.

The toolkit is a thin wrapper around the ScadaMiner remote MCP server
(`https://chat.scadaminer.com/mcp`). The server does the work; this repo just makes
it easy to add.

---

## Install

Pick the path that matches how you use Claude.

### Claude Code — plugin (recommended)

Adds the connector **plus** NEM-specific slash commands and a pre-prompted NEM
analyst subagent.

```
/plugin marketplace add brensch/scadaminer-ai-toolkit
/plugin install scadaminer@scadaminer
```

You'll be prompted to sign in (OAuth) the first time Claude uses a ScadaMiner tool.

### Claude Code — connector only (one-liner)

Just the MCP connection, no extra commands:

```
claude mcp add --transport http scadaminer https://chat.scadaminer.com/mcp
```

### Claude.ai / Claude Desktop — custom connector

1. Settings → **Connectors** → **Add custom connector**
2. Paste the URL: `https://chat.scadaminer.com/mcp`
3. Click **Add**, then sign in when prompted.

See [docs/connectors.md](docs/connectors.md) for screenshots-level detail and
Team/Enterprise notes.

---

## What you get (Claude Code plugin)

**Slash commands** (mirror the server's real workflow):

| Command | What it does |
|---------|--------------|
| `/scadaminer:nem-price` | Spot / FCAS price over a region and period |
| `/scadaminer:nem-generation` | Generation output for a DUID, station, fuel, or region |
| `/scadaminer:duid-lookup` | Resolve a station or DUID and show its facts |
| `/scadaminer:nem-capabilities` | List the validated question shapes the warehouse answers |

**Subagent:** `nem-analyst` — a focused agent that follows the ScadaMiner
capability-first workflow (resolve entities → prefer a validated capability →
fall back to hand-written SQL → chart → cite numbers).

---

## Agent Skills

Skills live in [`skills/`](skills/) and can be used with the ScadaMiner MCP
server in any Skills-capable Claude surface.

| Skill | Description |
|-------|-------------|
| [`nem-market-analysis`](skills/nem-market-analysis/SKILL.md) | Answer Australian NEM / AEMO questions (prices, FCAS, generation, interconnectors, constraints, demand, bids, revenue) via the ScadaMiner MCP server: resolve entities, prefer validated query capabilities, write safe read-only SQL only as a fallback, and return cited numbers with charts. |

---

## How it works

ScadaMiner is a remote [MCP](https://modelcontextprotocol.io) server with OAuth.
Its tools: `search_entities`, `get_data_freshness`, `list_tables`,
`search_columns`, `get_table_schema`, `execute_sql`, `list_capabilities`,
`run_capability`, `build_chart`, `get_concept`, plus `start_question` for
grouping a turn's calls into one auditable trace.

This repo contributes only configuration and prompts — no code runs locally.

## Links

- App: https://chat.scadaminer.com
- MCP endpoint: https://chat.scadaminer.com/mcp
- Issues / requests: https://github.com/brensch/scadaminer-ai-toolkit/issues
