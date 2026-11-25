# Hormouz MCP

[![Hormouz MCP connector](https://glama.ai/mcp/connectors/net.hormouz/mcp/badges/score.svg)](https://glama.ai/mcp/connectors/net.hormouz/mcp)

A read-only MCP server for [Hormouz](https://hormouz.net) customers. It lets an AI assistant — Claude, Cursor, or any MCP client — read your Hormouz account in plain language: balance, API-key status, usage statistics and request logs. It also walks you through connecting a coding or chat client.

It is **read-only**. It never calls a model and never spends credit, so the key you give it is safe to paste into a client — the worst a leak can do is let someone read your usage, not spend your money.

> **What is Hormouz?** A unified AI API: reach many leading AI models — chat, coding, images, audio — through one fast, reliable, OpenAI-compatible API, and pay for all of them in one place.

The server is **remote** (Streamable HTTP) and already live at `https://api.hormouz.net/mcp`. There is nothing to install; you point a client at the URL with a read-only key.

## Get a read-only key

In the Hormouz dashboard: **Keys → Create → Read-only account key**. The key has scope `account:read` and cannot spend.

## Connect

**Claude Code**
```
claude mcp add --transport http hormouz https://api.hormouz.net/mcp \
  --header "Authorization: Bearer ng-YOUR_READONLY_KEY"
```

**Cursor / generic** (`mcp.json`)
```json
{
  "mcpServers": {
    "hormouz": {
      "url": "https://api.hormouz.net/mcp",
      "headers": { "Authorization": "Bearer ng-YOUR_READONLY_KEY" }
    }
  }
}
```

## Tools

All nine are read-only.

| Tool | What it returns |
|---|---|
| `get_balance` | balance, credit line, spend today / this month |
| `get_key` | status, limits and spend of the calling key |
| `list_keys` | every key with its limits and spend |
| `get_usage_stats` | usage grouped by day / month / model / key / API shape |
| `get_usage_logs` | recent request logs |
| `list_models` | models the key can use |
| `get_connection_info` | base URLs and the auth pattern |
| `get_code_setup` | steps to connect a coding client to Hormouz Code |
| `get_chat_setup` | steps to set up a chat client on Hormouz |

## Ask it things like

- What's my Hormouz balance?
- How much have I spent this month?
- Show my API keys.
- Which models do I use most?
- How do I set up Hormouz Code in my editor?
- Connect a chat client to Hormouz.

## Links

- Guide: https://docs.hormouz.net/guides/mcp
- Registry manifest: [`server.json`](./server.json)
- Hormouz: https://hormouz.net
