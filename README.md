# KeyShortcuts MCP Server

A free, stateless Model Context Protocol (MCP) server for keyboard shortcuts — hosted at **https://keyshortcuts.net/api/mcp**. No API key, no sign-in, no rate-limit paywall for basic use.

Search 2,719 verified shortcut records across 7 platforms (Windows, macOS, Linux, ChromeOS, iOS, Android) and 45 apps (VS Code, Excel, Figma, Photoshop, Notion, Slack, Vim, IntelliJ IDEA, Cursor, and more) — or look up what a key combination does, compare across platforms, and translate bindings between Windows/macOS.

## Quick start

Add to your MCP client config:

```json
{
  "mcpServers": {
    "keyshortcuts": {
      "type": "http",
      "url": "https://keyshortcuts.net/api/mcp"
    }
  }
}
```

### Claude Desktop / Claude Code

```bash
claude mcp add keyshortcuts --transport http https://keyshortcuts.net/api/mcp
```

## Available tools

| Tool | Description |
| --- | --- |
| `search_shortcuts` | Search action meanings and app labels |
| `list_apps` | List supported apps and platforms |
| `get_app_shortcuts` | Get the shortcut records for one app |
| `lookup_shortcut` | Look up what a literal key combination does |
| `compare_platforms` | Reviewed equivalents of an action across platforms |
| `translate_shortcut` | Translate a binding between platforms (e.g. Windows → macOS) |
| `get_source` | Source and review metadata for a binding |
| `create_shortcut_set` | Compose a custom shortcut set |

Every record carries **source references and per-binding review status** — shortcuts are facts, but which ones are confirmed for your platform matters. The server never guesses platform translations.

## Verify it right now

```bash
curl -s https://keyshortcuts.net/api/mcp \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-03-26","capabilities":{},"clientInfo":{"name":"curl","version":"1.0"}}}'
```

## REST API

The same dataset is available as a plain REST API (free, 60 req/min/IP):

- `GET /api/apps` — list apps
- `GET /api/search?q=...` — search shortcuts
- `GET /api/keys/{combination}` — lookup a literal key combination
- `GET /api/compare?id=...` — reviewed cross-platform equivalents
- `GET /api/translate?id=...&from=windows&to=macos` — translate a binding
- `GET /api/sources/{sourceId}` — source and review metadata
- Schema: https://keyshortcuts.net/api/openapi.json

Example:

```bash
curl "https://keyshortcuts.net/api/search?q=reopen%20closed%20tab&limit=2"
```

## Free web tools

- [Shortcut finder](https://keyshortcuts.net/#shortcut-finder) — search by action or by keys
- [My Stack](https://keyshortcuts.net/my-stack) — build your personal shortcut stack
- [Windows ↔ Mac switcher](https://keyshortcuts.net/switcher)
- [Practice quiz](https://keyshortcuts.net/quiz) — test and build your shortcut memory
- [Free PDF](https://keyshortcuts.net) — 50 essential shortcuts
- [Premium PDF packs](https://keyshortcuts.net/shop) — from $4

## Attribution

We make no proprietary claim over keyboard combinations — they are facts about software. Our contribution is the curation, review status, and source references. Please keep the attribution link when reusing the data.
