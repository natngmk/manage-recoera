# manage-recoera

Claude Code workspace for managing the Recoera e-commerce store. Connectors, skills, agents and plugins
are all stored in this repo (project scope), so they only load when Claude Code runs in this folder, and
any machine that clones the repo gets the same setup.

## 1. Install on the laptop

| Tool | Why | Install (macOS) |
|------|-----|-----------------|
| Claude Code | The AI assistant | `npm install -g @anthropic-ai/claude-code` or see claude.com/claude-code |
| git | Version control | `xcode-select --install` |
| GitHub CLI | PRs from the terminal | `brew install gh` then `gh auth login` |
| Shopify CLI | Used by the Shopify plugin to manage the store | `npm install -g @shopify/cli` |
| Node.js | Runs most MCP connectors (`npx`) | `brew install node` |
| direnv | Loads `.env` secrets automatically | `brew install direnv`, then add `eval "$(direnv hook zsh)"` to `~/.zshrc` |
| uv (optional) | Runs Python-based MCP connectors | `brew install uv` |

## 2. Set up secrets

```sh
cp .env.example .env     # then fill in the values
direnv allow             # once, so .env loads when you cd into this folder
```

`.env` is gitignored, so set it up on each machine.

## 3. Connect Shopify (once per laptop)

See `docs/connectors.md` → *Shopify setup* for the `shopify store auth` command.

## 4. Start

```sh
cd manage-recoera
claude
```

Inside Claude Code:
- `/mcp`: check that the connectors are connected
- `/skills`: list the project skills
- `/plugin`: browse the local `recoera-local` plugin marketplace

## What's in here

| Path | What |
|------|------|
| `CLAUDE.md` | Business context and rules Claude follows (fill in the TODOs) |
| `.mcp.json` | Connectors (MCP servers) for this project |
| `.claude/settings.json` | Shared permissions, connector and plugin settings |
| `.claude/skills/` | Skills: `product-listing`, `order-report`, `inventory-check`, `customer-reply` |
| `.claude/agents/` | Subagents: `store-ops` |
| `plugins/` | In-repo plugin marketplace |
| `docs/connectors.md` | Connector list and **how to add a new one** (store, Gmail, Sheets…) |
| `docs/brand-voice.md` | Tone and formatting for customer-facing text |
| `data/` | Reports and exports. `data/private/` is gitignored |

## Next steps
1. Fill in `CLAUDE.md` (what you sell, platform) and `docs/brand-voice.md`.
2. Add the store platform connector by following `docs/connectors.md`.
