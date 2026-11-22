# Connectors

Connectors are MCP servers defined in `.mcp.json` at the repo root. They load **only** when you run
`claude` inside this folder. Secrets come from environment variables set in `.env` (gitignored), which
direnv loads automatically.

## Current connectors

| Name | Purpose | Status |
|------|---------|--------|
| _(none yet)_ | | |

## How to add a connector (e.g. store platform, Gmail, Google Sheets)

1. Find the MCP server for the app (official docs, or https://github.com/modelcontextprotocol/servers).
2. Add an entry to `.mcp.json`, referencing secrets as `${VAR_NAME}`:
   ```json
   {
     "mcpServers": {
       "store": {
         "command": "npx",
         "args": ["-y", "<mcp-server-package>"],
         "env": {
           "STORE_DOMAIN": "${STORE_DOMAIN}",
           "STORE_API_TOKEN": "${STORE_API_TOKEN}"
         }
       }
     }
   }
   ```
   For a hosted (remote) server, use `{ "type": "http", "url": "https://...", "headers": { ... } }` instead.
3. Add the variable **names** to `.env.example`, then put the real **values** in `.env`.
4. Install any CLI the server needs (e.g. Node for `npx`, `uv` for Python servers). Note it in the README.
5. Restart `claude` in this folder and run `/mcp` to check it's connected.
6. Add a row to the table above.

### Local connector vs claude.ai connector
- **Local (default):** defined in `.mcp.json`, so it's scoped to this repo. It needs your own API
  credentials (e.g. Gmail requires creating a Google Cloud OAuth client once).
- **claude.ai connector:** one-click setup in claude.ai → Settings → Connectors, but it's tied to your
  account and appears in **every** project. Only use this if you're fine with that.
