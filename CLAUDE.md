# Menu Decoder — Assistant Primer

> This file is loaded automatically by Claude as project-level context.

---

## Project identity
**What it is:** A restaurant menu translator that decodes foreign-language menus into English with cultural context, ingredient icons, and order sharing
**Phase:** HTML prototype → macOS/iOS app (Swift/SwiftUI)
**Remote:** `https://github.com/marybendev69/menu-decoder.git`
**GitHub account:** `marybendev69`
**Push method:** HTTPS via `gh` CLI (authenticated on Trullo Dolce)
**Live site:** https://marybendev69.github.io/menu-decoder/

---

## Session start — always run live, never assume
```bash
cd ~/Developer/Personal/MenuDecoder/menu-decoder
git status
git log --oneline -8
git branch -a
```

---

## Development environment

**CRITICAL:** Use `mcp__shell__cli-exec-raw` for ALL git and gh operations.
The Cowork sandbox has no network access to GitHub. The shell MCP tool runs
directly on Trullo Dolce as `alexguidice` with full `gh` CLI access.

- **Edit files** via the mounted path: `/sessions/blissful-clever-fermat/mnt/MenuDecoder/menu-decoder/`
- **Git/push** via shell MCP: `mcp__shell__cli-exec-raw` → runs on host machine
- **gh CLI** is authenticated as `marybendev69` with repo + workflow scopes
- **GitHub Pages** deploys from `main` branch at root (Deploy from branch)

### Workflow
1. Edit files using Read/Write/Edit tools on the mounted path
2. Commit and push using `mcp__shell__cli-exec-raw`:
   ```bash
   cd ~/Developer/Personal/MenuDecoder/menu-decoder && git add <files> && git commit -m "<msg>" && git push origin main
   ```
3. GitHub Pages auto-deploys from main

---

## Architecture (current: HTML prototype)

```
menu-decoder/
├── index.html              # Landing page — menu directory
├── menus/
│   └── cipolla-doro.html   # Tabbed: Claude vs Foundation Model decode
├── docs/
│   ├── ARCHITECTURE.md     # System architecture
│   └── PROJECT-BOARD.md    # Feature roadmap
├── src/                    # (Future) JS modules
├── .github/workflows/
│   └── pages.yml           # GitHub Pages deployment
└── .nojekyll               # Bypass Jekyll processing
```

### Tabbed comparison system
Each menu page has two tabs:
- **Claude Decoded** (Tab 1): Full menu decoded by Claude with translations, cultural context, ingredient icons, and About section
- **Foundation Model** (Tab 2): Template with `data-section` attributes for Apple Intelligence to populate. Schema defined in `window.MenuDecoderSchema`

### Data schema
Menu items follow this structure (see `window.MenuDecoderSchema` in menu HTML):
```json
{
  "name_it": "string",
  "name_en": "string (UPPERCASE)",
  "price": "string (e.g. €13)",
  "description": "string",
  "ingredients": ["beef", "cheese", ...],
  "tags": ["house-pick", "shareable"],
  "cultural_context": "string"
}
```

---

## Key sealed decisions — do not reverse without explicit discussion
- HTML-first prototyping before Swift/SwiftUI app
- Tabbed comparison: Claude vs Apple Foundation Model on same menu
- Decode once, save permanently (not re-decode on every view)
- `data-section` attributes on Foundation Model tab for programmatic population
- GitHub Pages for sharing prototypes (Heather can view live)
- Order sharing via iMessage/Mail (native iOS integration path)

---

## Future roadmap
1. **macOS/iOS app** — Swift/SwiftUI with Apple Foundation Model integration
2. **Menu import** — Apple Maps, Google Maps, browser extension (Paprika-style)
3. **Foundation Model comparison** — A/B test Claude vs Apple Intelligence quality
4. **Offline decode** — On-device Foundation Model for restaurant use without WiFi

---

## Key docs in this project
| File | What it governs |
|---|---|
| `CLAUDE.md` | This file — AI assistant context |
| `README.md` | Project overview |
| `docs/ARCHITECTURE.md` | System design |
| `docs/PROJECT-BOARD.md` | Feature roadmap |
| `CHANGELOG.md` | Behaviour changes |
| `DEVLOG.md` | Session log |
