# LucidNest MCP Server


Connect AI assistants (Claude, agents) to your [LucidNest](https://lucidnest.io) workspace
via the Model Context Protocol — 18 tools to manage todos, notes, notebooks, projects and quotes.

## Quick start

1. Create a scoped token at **lucidnest.io → Settings → Tokens MCP**
   (pick only the scopes you need: `todos:read`, `notes:write`, …).
2. Add the server to your client:

### Claude Desktop / Claude Code (`mcpServers`)

```json
{
  "mcpServers": {
    "lucidnest": {
      "type": "http",
      "url": "https://lucidnest.io/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN"
      }
    }
  }
}
```

Transport : **Streamable HTTP** (spec MCP `2025-06-18`, versions négociées :
`2024-11-05`, `2025-03-26`, `2025-06-18`). Endpoint unique `POST /mcp`.

## Tools (18)

| Domain | Tools | Scope |
|---|---|---|
| Todos | `create_todo`, `list_todos`, `complete_todo`, `delete_todo`, `get_myday` | `todos:read/write/delete` |
| Notes | `create_note`, `search_notes`, `delete_note` | `notes:read/write/delete` |
| Notebooks | `list_notebooks`, `manage_tabs`, `delete_notebook` | `notebooks:read/write/delete` |
| Projects | `list_projects`, `create_project`, `delete_project` | `projects:read/write/delete` |
| Quotes | `list_quotes`, `create_quote`, `delete_quote` | `quotes:read/write/delete` |
| Profile | `get_profile` | `user:read` |

## Security

- Scoped Sanctum tokens (least privilege), revocable anytime from Settings.
- Per-scope rate limits: 60 reads/min, 10 writes/min.
- All deletions are soft-deletes (recoverable from Trash).

## License

MIT (wrapper/reference only — the LucidNest platform itself is proprietary).
