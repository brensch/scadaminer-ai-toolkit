# NEM Explorer for Claude

Connect your AI agent to **NEM Explorer** by [SCADA Miner](https://chat.scadaminer.com),
a data warehouse for Australia's National Electricity Market (NEM). Ask questions
about AEMO market data in plain English (spot and FCAS prices, generation,
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

**Claude Desktop app (Windows / Mac)**

The desktop app adds marketplaces through its own menu, not `/plugin`.

1. Open **Customize → Plugins** (or Settings → Plugins).
2. Click **+ Add → Add marketplace** and enter `brensch/scadaminer-ai-toolkit`.
3. On the **Discover** tab, search **NEM Explorer** and click **Add**.
4. Open the plugin's **Connectors** tab, click **Connect**, and sign in.

Requires Claude Pro, Max, Team, or Enterprise. The plugin is saved to your
claude.ai account, so it also shows up in Claude Code sessions, chat, and Cowork.

**Claude Code CLI**

Inside a session (v2.1.275 or later):

```
/plugin install scadaminer --marketplace brensch/scadaminer-ai-toolkit
```

Or from your shell:

```
claude plugin marketplace add brensch/scadaminer-ai-toolkit
claude plugin install scadaminer@scadaminer
```

Without the plugin:

```
claude mcp add --transport http scadaminer https://chat.scadaminer.com/mcp
```

**Claude.ai (connector only)**

Settings → Connectors → Add custom connector → paste
`https://chat.scadaminer.com/mcp` → sign in. On Team/Enterprise plans an owner
adds it under Organization settings first.

**Any other MCP client**

Add a remote (streamable HTTP) server with the URL above.

## Links

- App: https://chat.scadaminer.com
- Issues: https://github.com/brensch/scadaminer-ai-toolkit/issues
