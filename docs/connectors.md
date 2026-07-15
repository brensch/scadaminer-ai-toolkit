# Adding SCADA Miner as a custom connector

For **Claude.ai (web)** and **Claude Desktop** users. (Claude Code users should
use the [plugin](../README.md#claude-code--plugin-recommended) instead.)

The connector URL is:

```
https://chat.scadaminer.com/mcp
```

SCADA Miner uses OAuth — you'll sign in through a browser window the first time.
Because the server supports Dynamic Client Registration, you do **not** need to
paste a client ID or secret.

## Pro / Max plans

1. Open **Settings** → **Connectors** (also reachable via **Customize →
   Connectors**).
2. Click **Add custom connector**.
3. Enter the URL `https://chat.scadaminer.com/mcp`.
4. Click **Add**, then **Connect** and complete the sign-in prompt.

## Team / Enterprise plans

A workspace **Owner** must enable the connector first:

1. **Organization Settings** → **Connectors** → **Add** → **Custom** → **Web**.
2. Enter `https://chat.scadaminer.com/mcp` and save.
3. Each member then connects individually under their own **Connectors** settings
   and signs in.

## Using it

Once connected, just ask NEM questions in chat — e.g. "What was the average NSW1
spot price last week?" or "Compare black coal vs wind generation in QLD1
yesterday." Claude will call the SCADA Miner tools to resolve entities, run
validated queries, and chart the results.

## Troubleshooting

- **Sign-in loop / no tools appear:** remove and re-add the connector; ensure the
  URL ends in `/mcp`.
- **"Connector unavailable":** the service may be briefly down — retry, or check
  https://chat.scadaminer.com.
