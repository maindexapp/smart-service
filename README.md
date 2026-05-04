# Maindex Smart MCP Server

This is the official Maindex Smart MCP server published by [Maindex](https://maindex.io).

Maindex Smart is a hosted remote MCP service. No local installation is required.

[Website](https://maindex.io) | [Help & FAQ](https://maindex.io/help) | [Dashboard](https://maindex.io/dashboard)

Maindex Smart provides simple, user-controlled memory for AI assistants. It exposes four explicit tools for keeping, recalling, updating, and forgetting information across sessions. There is no hidden automatic collection — every memory operation is initiated by you or your agent. Safe defaults are built in: LLM rewriting is off unless explicitly requested, and irreversible wipes require explicit confirmation.

Both Smart and Expert services are included with every Maindex plan at no additional cost. They read and write the same memory graph, and you can switch between them or use both simultaneously.

## Endpoint

`https://maindex.io/mcp`

## Tools

- `keep` — store a memory with optional headline, tags, and collections.
- `recall` — search and retrieve memories using relevant, exact, current_state, history, or recent modes.
- `update` — update an existing memory by `mem-*` ID.
- `forget` — soft-delete a memory by `mem-*` ID, or permanently wipe history only with explicit irreversible confirmation.

## Installation

Use the hosted endpoint in any MCP client that supports remote streamable HTTP MCP servers.

```json
{
  "mcpServers": {
    "maindex": {
      "url": "https://maindex.io/mcp"
    }
  }
}
```

Or install a platform-specific plugin:

| Platform | How to connect |
|---|---|
| **Cursor** | Install [cursor-smart-plugin](https://github.com/maindexapp/cursor-smart-plugin) from the Plugin Marketplace |
| **Claude** | Install [claude-smart-plugin](https://github.com/maindexapp/claude-smart-plugin) |
| **Gemini** | Install [gemini-smart-plugin](https://github.com/maindexapp/gemini-smart-plugin) as a Gemini Extension |
| **OpenClaw** | Install [openclaw-smart-plugin](https://github.com/maindexapp/openclaw-smart-plugin) from the Plugin Registry |

## Example Usage

- `Keep this preference: I prefer TypeScript for backend examples.`
- `Recall my language preferences.`
- `Update mem-abc123 to say I also like Rust.`
- `Forget mem-abc123.`

## Safety and Control

- `keep` stores user-provided content. No data is collected automatically.
- `recall` is read-only.
- `update` and `forget` require explicit `mem-*` targets.
- `rewrite` defaults to false and performs zero LLM rewriting unless explicitly set to true.
- `wipe_history` is irreversible and requires `confirm_irreversible_wipe=true`.

---

## Authentication

Maindex uses **OAuth 2.1** for all connections. MCP clients handle the OAuth flow automatically — on first use, a browser window opens for sign-in and authorization.

For headless environments, API keys with per-key revocation are available from your [dashboard](https://maindex.io/dashboard).

---

## FAQ

### Why not use my LLM's built-in memory?

Built-in LLM memory is typically a flat list of text notes with no structure, no search beyond keyword matching, and no way to export or move your data to another service. If you switch providers, your memories stay behind.

Maindex gives you a structured, searchable memory graph accessible through both an agent-facing MCP interface and a human-facing dashboard. Your data is portable across every platform that supports MCP.

### Should I use Smart or Expert?

Both are included, both read and write the same memory graph, and you can switch at any time. Smart is optimized for simple user-controlled memory. Expert is optimized for capable agents that need direct control over the full memory graph.

See the [Expert service](https://github.com/maindexapp/expert-service) for the full-fidelity 14-tool API.

### What are synapses?

A synapse is a single unit of memory usage. Every time an agent or API call reads from or writes to your memory graph, the processing is measured in synapses. Your plan includes a generous monthly quota that resets each billing period. Check your usage on the [dashboard](https://maindex.io/dashboard).

### Can I export my data?

Yes. Your dashboard has three export options:
- **Full Export** (JSON): memories, tags, collections, links, revision history, conversations — everything
- **Memories JSON**: clean memory-only JSON
- **Memories CSV**: spreadsheet-friendly format

You can also import a Full Export JSON back into a new account.

### Is my data private?

Every account is a fully isolated tenant. Your data is never shared, mixed, or accessible by other users. All data is encrypted at rest (AES-256) and in transit (TLS 1.2+). Maindex does not train models on your data.

---

## Plugin Repos

| Platform | Plugin |
|---|---|
| Cursor | [cursor-smart-plugin](https://github.com/maindexapp/cursor-smart-plugin) |
| Claude | [claude-smart-plugin](https://github.com/maindexapp/claude-smart-plugin) |
| Gemini | [gemini-smart-plugin](https://github.com/maindexapp/gemini-smart-plugin) |
| OpenClaw | [openclaw-smart-plugin](https://github.com/maindexapp/openclaw-smart-plugin) |

## See Also

- [Expert Service](https://github.com/maindexapp/expert-service) — 14 tools + 6 resources for full graph control
- [maindex.io](https://maindex.io) — Dashboard and account management
- [Help & FAQ](https://maindex.io/help)

## License

MIT
