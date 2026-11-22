# Connectors

Connectors are MCP servers defined in `.mcp.json` at the repo root. They load **only** when you run
`claude` inside this folder. Secrets come from environment variables set in `.env` (gitignored), which
direnv loads automatically.

## Current connectors

| Name | Purpose | Status |
|------|---------|--------|
| Shopify AI Toolkit (plugin) | Shopify docs/schemas, GraphQL validation, live store reads/writes via Shopify CLI | Enabled — run `shopify store auth` once per laptop |

## Shopify setup (per laptop)

The official plugin `shopify-ai-toolkit@claude-plugins-official` is enabled in `.claude/settings.json`, so
opening `claude` here offers to install it. It has no MCP server; it uses Shopify CLI.

1. Shopify CLI installed (`shopify version`).
2. Authenticate the CLI against the store once (opens a browser):
   ```sh
   shopify store auth -s <your-store>.myshopify.com \
     --scopes read_products,write_products,read_orders,read_inventory,write_inventory,read_locations,read_customers,read_reports
   ```
   Add or remove scopes as needed. Write scopes let Claude propose changes, and each `store execute`
   call still asks for permission.
3. Check it works: in `claude`, ask "show the first 5 products on my store".

Telemetry: the plugin's skill scripts send usage data (queries, code) to shopify.dev by default. To opt
out, set `OPT_OUT_INSTRUMENTATION=true` or create `~/.config/shopify-ai-toolkit/opt-out`.

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
