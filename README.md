# Maindex Smart

**Persistent, relational memory for AI agents and their humans.**

Maindex Smart is the streamlined MCP interface — four intuitive tools that give any AI agent long-term memory. Behind the scenes, Smart routing handles retrieval strategy, ambiguity resolution, and content shaping so the agent doesn't have to.

Both Smart and Expert services are included with every Maindex plan at no additional cost. They read and write the same memory graph, and you can switch between them or use both simultaneously.

**MCP Endpoint:** `https://maindex.io/mcp`

---

## Quick Start

### 1. Connect your agent

Add the Maindex Smart MCP server to your AI platform of choice:

| Platform | How to connect |
|---|---|
| **Cursor** | Install [cursor-smart-plugin](https://github.com/maindexapp/cursor-smart-plugin) from the Plugin Marketplace |
| **Claude** | Install [claude-smart-plugin](https://github.com/maindexapp/claude-smart-plugin) |
| **Gemini** | Install [gemini-smart-plugin](https://github.com/maindexapp/gemini-smart-plugin) as a Gemini Extension |
| **OpenClaw** | Install [openclaw-smart-plugin](https://github.com/maindexapp/openclaw-smart-plugin) from the Plugin Registry |
| **Any MCP client** | Point your MCP client at `https://maindex.io/mcp` (Streamable HTTP transport, OAuth 2.1) |

### 2. Authenticate

On first connection, you'll be redirected to [maindex.io](https://maindex.io) to sign in and authorize. OAuth handles the rest.

### 3. Start remembering

Ask your agent to remember something, and it will use the `keep` tool. Ask a question about your past work, and it will use `recall`. That's it — four tools, no configuration.

---

## Tools

| Tool | What it does |
|---|---|
| **`keep`** | Store a new memory. Provide `content` (required), optionally `headline`, `tags`, `collections`, `metadata`. Opt into LLM-assisted rewriting with `rewrite: true`. |
| **`recall`** | Search and retrieve memories. Modes: `relevant` (semantic search), `exact` (literal match), `current_state` (latest revision), `history` (revision trail), `recent` (newest first). Filter by `tags` and `collections`. |
| **`update`** | Revise an existing memory by `target_id` (mem-* short ID). Change `content`, `headline`, `tags`, or `metadata`. Each update creates a new revision — full history is preserved. |
| **`forget`** | Remove a memory by `target_id`. Default is a safe, reversible soft-delete. With `wipe_history: true` + `confirm_irreversible_wipe: true`, permanently purges all revisions. |

---

## REST API

The same four operations are available as REST endpoints for programmatic access:

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/v1/keep` | Create a memory |
| `POST` | `/v1/recall` | Search/retrieve memories |
| `POST` | `/v1/update` | Update a memory |
| `POST` | `/v1/forget` | Delete a memory |

Request bodies match the MCP tool inputs exactly. All endpoints require OAuth 2.1 bearer tokens.

**Base URL:** `https://maindex.io`

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

Both are included, both read and write the same memory graph, and you can switch at any time. Use **Smart** when you want the agent to send high-level intents and let the pipeline decide. Use **Expert** when the agent needs direct, granular control over memory operations.

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
- [Documentation](https://docs.maindex.io)
