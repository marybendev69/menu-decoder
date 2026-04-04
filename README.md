# Menu Decoder 🍽️

**Instantly understand any restaurant menu in any language.**

Translates foreign menus into English with ingredient icons, cultural context, preparation notes — and lets you tap dishes to share your order via iMessage or email.

## Live Demo

**[aguidice.github.io/menu-decoder](https://aguidice.github.io/menu-decoder)**

Currently featuring: **La Cipolla d'Oro** — a B&B and Ristorante in Ancona, Le Marche, Italy.

## What It Does

- **Translates** every dish name and description into English with cultural context
- **Ingredient icons** (emoji-based) — spot fish 🐟, meat 🐄, shellfish 🦐, cheese 🧀, truffle 🍄, vegetarian 🌿 at a glance
- **Tap to select** dishes, then share your order via iMessage 💬, Apple Mail ✉️, or clipboard 📋
- **Responsive** — works on any phone at the table

## Project Structure

```
menu-decoder/
├── index.html              # Landing page + menu gallery
├── menus/
│   └── cipolla-doro.html   # Full decoded menu (first restaurant)
├── src/
│   ├── css/                # Shared styles (future)
│   ├── js/                 # Menu decoder engine (future)
│   └── data/               # Menu data as JSON (future)
├── docs/
│   ├── ARCHITECTURE.md     # App architecture and tech decisions
│   └── PROJECT-BOARD.md    # GitHub project board issue templates
└── .github/
    └── workflows/          # CI/CD (future)
```

## Roadmap

### Phase 1 — Static Decode ✅
Hand-crafted HTML menus with emoji icons and sharing. Hosted on GitHub Pages.

### Phase 2 — URL Ingestion
Paste a digital menu URL (leggimenu.it, thefork, etc.) → auto-scrape → AI translate → generate styled page.

### Phase 3 — Photo to Menu (OCR + AI)
Camera capture → OCR text extraction → AI translation + ingredient classification → styled output.

### Phase 4 — Native iOS App (Swift)
Camera integration, offline menu caching, dietary filters, Apple Wallet pass for saved menus.

### Phase 5 — Multi-Language
Support any source language → any target language. Japanese, Thai, French, Greek, Arabic, etc.

## Tech Stack

**Current:** Pure HTML/CSS/JS, GitHub Pages, Google Fonts, native emoji icons

**Planned:**
- **Frontend:** React or vanilla JS SPA
- **AI/Translation:** Claude API for contextual translation + ingredient classification
- **OCR:** Apple Vision framework (iOS) or Tesseract.js (web)
- **Backend:** Cloudflare Workers or Vercel Edge Functions
- **iOS:** SwiftUI + Vision framework + CoreML

## Getting Started

```bash
# Clone the repo
git clone https://github.com/Aguidice/menu-decoder.git
cd menu-decoder

# Open locally
open index.html

# Or serve with any static server
npx serve .
```

## Contributing

This project is in early alpha. Ideas, translations, and menu contributions welcome!

## License

MIT

---

*Built with Claude at La Cipolla d'Oro, Ancona, Italy — April 2026*
