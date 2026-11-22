# Recoera — e-commerce management workspace

This repo is the working folder for managing the Recoera online store with Claude Code.
All connectors, skills, agents and plugins live in this repo (project scope), not in `~/.claude`.

## Business context
<!-- TODO: fill in -->
- **What Recoera sells:** _TBD_
- **Store platform:** Shopify, store `ebdk0r-tb.myshopify.com` (shop name "My Store 3", trial plan)
- **Currency:** SGD
- **Main sales channels:** _TBD_

## Where things live
- Shopify: official **Shopify AI Toolkit** plugin (enabled in `.claude/settings.json`). It manages the store
  through Shopify CLI (`shopify store auth` / `shopify store execute`). `store execute` always asks for permission.
- Connectors (MCP servers): `.mcp.json`. See `docs/connectors.md` for what each one is and how to add more.
- Skills: `.claude/skills/<name>/SKILL.md`
- Subagents: `.claude/agents/`
- In-repo plugins: `plugins/` (local marketplace `recoera-local`)
- Brand voice: `docs/brand-voice.md`
- Reports and exports Claude produces: `data/`. Anything sensitive (customer data) goes in `data/private/` (gitignored).

## Working rules
1. **Confirm before writing to the live store.** Show the exact change (product, field, old → new) and wait
   for a yes before changing prices, stock, product content, orders, refunds or customer records.
2. **Never commit secrets.** Credentials go in `.env` only. Never read, print or copy `.env` values.
3. **Follow the brand voice** in `docs/brand-voice.md` for anything customer-facing.
4. **Save outputs** (reports, CSVs, drafts) under `data/` with a dated filename, e.g. `data/2026-11-22-orders.md`.
5. **Don't invent data.** If a connector isn't set up or returns nothing, say so; don't make up numbers.
6. **Git:** `main` is protected. Make changes on a branch → PR → merge.
