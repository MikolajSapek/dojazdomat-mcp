# Dojazdomat MCP server

Remote MCP server for [Dojazdomat](https://dojazdomat.pl): commute time versus rent in Warsaw. Ask an AI assistant where you can rent cheaply and still get to work in 30 minutes by public transport.

Endpoint: `https://dojazdomat.pl/mcp` (Streamable HTTP, no sign-in, 60 requests per minute per IP).

## Tools

| Tool | What it returns |
|---|---|
| `find_place` | Transit stop groups and neighborhoods matching a name, with their lat/lon. |
| `commute_time` | Door-to-door minutes by public transport plus walking, weekday morning 7-9 average, same model as the map. |
| `rent_stats` | Asking-rent statistics (n, median, p25, p75) of rental ads within a radius of a point. |
| `rank_neighborhoods` | Warsaw neighborhoods ranked for a workplace by median rent, commute minutes or value (rent against the typical rent nearby). |
| `dataset_info` | Data dates, sources, listing counts per portal, method notes and caveats. |

Suggested flow: `find_place`, then `rank_neighborhoods`, then `rent_stats`.

The server returns aggregates only (a median needs at least 20 listings, p25 and p75 at least 10). It never returns single listings or their coordinates.

## Connect

**Cursor** and other clients that read `mcpServers`: copy [`mcp.json`](mcp.json) into `.cursor/mcp.json`.

**Claude Code:**

```bash
claude mcp add --transport http dojazdomat https://dojazdomat.pl/mcp
```

**Claude (claude.ai):** Settings, Connectors, Add custom connector, URL `https://dojazdomat.pl/mcp`.

**Codex** (`~/.codex/config.toml`):

```toml
[mcp_servers.dojazdomat]
url = "https://dojazdomat.pl/mcp"
```

This repo holds the client config only. The server itself is hosted by Dojazdomat.
