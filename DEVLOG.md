# Dev Log — Menu Decoder

Session-by-session log. Most recent entry first.

---

## 2026-04-04 — Initial setup and tabbed comparison

**Goal:** Set up GitHub repo, Pages deployment, and tabbed Claude vs Foundation Model comparison

**What was done:**
- Cloned repo from GitHub into ~/Developer/Personal/MenuDecoder/menu-decoder
- Pushed project structure (docs, menus, .gitignore) to GitHub
- Enabled GitHub Pages (Deploy from branch, main, root)
- Built tabbed comparison page for Cipolla d'Oro menu:
  - Claude Decoded tab: full 100+ item menu with translations, ingredient icons, order sharing
  - Foundation Model tab: template with data-section attributes and MenuDecoderSchema
  - Added "About La Cipolla d'Oro" section with researched restaurant history
- Discovered shell MCP runs on host machine with full gh CLI access
- Created CLAUDE.md with development environment documentation
- Added GitHub Pages workflow (.github/workflows/pages.yml)

**Decisions:**
- Use mcp__shell__cli-exec-raw for all git/gh operations (sandbox has no GitHub network)
- Edit files via mounted path, push via shell MCP
- Decode once, save permanently (not re-decode per view)
- Tabbed A/B comparison architecture for Claude vs Foundation Model

**Outcome:** Completed — live site at marybendev69.github.io/menu-decoder/
