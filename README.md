# SCADA Miner AI Toolkit

Connect your AI agent to **[SCADA Miner](https://chat.scadaminer.com)**, a data
warehouse for Australia's National Electricity Market (NEM). Ask questions about
AEMO market data in plain English (spot and FCAS prices, generation,
interconnectors, constraints, bids, and more) and get answers with numbers and
charts.

Everything lives on the remote MCP server:

```
https://chat.scadaminer.com/mcp
```

This repo only points at it. The tools, their descriptions, and the workflow
guidance all come from the server, so they are always current. Sign-in is OAuth
with dynamic client registration; no keys to paste.

## Install

**Claude Code (plugin)**

```
/plugin marketplace add brensch/scadaminer-ai-toolkit
/plugin install scadaminer@scadaminer
```

**Claude Code (without the plugin)**

```
claude mcp add --transport http scadaminer https://chat.scadaminer.com/mcp
```

**Claude.ai / Claude Desktop**

Settings → Connectors → Add custom connector → paste
`https://chat.scadaminer.com/mcp` → sign in. On Team/Enterprise plans an owner
adds it under Organization settings first.

**Any other MCP client**

Add a remote (streamable HTTP) server with the URL above.

## Links

- App: https://chat.scadaminer.com
- Issues: https://github.com/brensch/scadaminer-ai-toolkit/issues
