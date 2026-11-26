# Hormouz MCP

[![Hormouz MCP connector](https://glama.ai/mcp/connectors/net.hormouz/mcp/badges/score.svg)](https://glama.ai/mcp/connectors/net.hormouz/mcp)

A read-only MCP server for [Hormouz](https://hormouz.net) customers. It lets an AI assistant — Claude, Cursor, or any MCP client — read your Hormouz account in plain language: balance, API-key status, usage statistics and request logs. It also walks you through connecting a coding or chat client.

It is **read-only**. It never calls a model, never spends credit and cannot change anything on your account.

### What a read-only key can see

The key has scope `account:read`, which reads the **whole account**. If it leaks, whoever holds it can see:

- **Balance:** current balance, credit line, and spend today and this month.
- **API keys:** every key's name, prefix (the first characters only), status, scopes, limits, allowed models and spend.
- **Request logs:** for each request, the time, model, API shape, status, tokens, cost, duration, request ID and the prefix of the key that made it.
- **Usage statistics:** spend, requests and tokens grouped by day, month, model, key or API shape.

It **cannot** see prompt or response content, full key secrets, or your email and phone number. It also cannot spend credit, call a model, or create, change or revoke keys. Treat it like any credential: keep it private, and revoke it in the dashboard if it leaks.

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

All nine are read-only. The full [`tools/list`](./tools-list.json) response is in this repo; it was captured from the live server with a test `account:read` key (the key itself is not published).

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
