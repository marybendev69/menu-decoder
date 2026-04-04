# Architecture — Menu Decoder

## Overview

Menu Decoder transforms foreign-language restaurant menus into rich, interactive English guides with ingredient classification, cultural context, and order sharing.

## Current State (v0.1 — Static)

```
User → opens GitHub Pages URL → browses pre-built HTML menu
                                  → taps dishes to select
                                  → shares via iMessage / Mail / clipboard
```

Everything is client-side HTML/CSS/JS. No backend. No build step.

## Target Architecture (v1.0)

```
┌─────────────────────────────────────────────────────┐
│                    CLIENT                            │
│  ┌──────────┐  ┌──────────┐  ┌───────────────────┐  │
│  │ Camera / │  │  URL     │  │  Menu Viewer      │  │
│  │ Photo    │  │  Input   │  │  + Selector        │  │
│  │ Capture  │  │          │  │  + Share (SMS/Mail)│  │
│  └────┬─────┘  └────┬─────┘  └───────────────────┘  │
│       │              │                ▲               │
│       ▼              ▼                │               │
│  ┌──────────────────────────┐        │               │
│  │     Menu Ingestion       │        │               │
│  │  OCR → Raw Text → JSON  │────────┘               │
│  └────────────┬─────────────┘                        │
└───────────────┼──────────────────────────────────────┘
                │
                ▼
┌───────────────────────────────────┐
│           AI LAYER                │
│  ┌─────────────────────────────┐  │
│  │  Claude API                 │  │
│  │  • Translate dish names     │  │
│  │  • Classify ingredients     │  │
│  │  • Generate descriptions    │  │
│  │  • Cultural context notes   │  │
│  │  • Dietary flag detection   │  │
│  └─────────────────────────────┘  │
└───────────────────────────────────┘
                │
                ▼
┌───────────────────────────────────┐
│         OUTPUT LAYER              │
│  • Styled HTML (GitHub Pages)     │
│  • JSON data (for app consumption)│
│  • Shareable text (SMS/Mail)      │
│  • PDF export (future)            │
└───────────────────────────────────┘
```

## Key Design Decisions

### 1. Emoji Icons over Icon Fonts
**Decision:** Use native emoji for ingredient classification instead of an icon font library.

**Rationale:**
- Zero external dependencies (no Font Awesome, no CDN)
- Renders natively on Apple devices (beautiful on iOS/macOS)
- Universal — works on every device/browser without loading
- Fun, approachable aesthetic that matches the use case
- Easy to extend — just add more emoji

**Icons:** 🐄 Beef, 🐷 Pork, 🐑 Lamb, 🐔 Poultry, 🦌 Game, 🐟 Fish, 🦐 Shellfish, 🧀 Cheese, 🥓 Cured Meats, 🍄 Truffle, 🌿 Vegetarian

### 2. Static-First, Progressive Enhancement
**Decision:** Start with pure static HTML. Add interactivity layer by layer.

**Rationale:**
- Works offline (important when traveling with spotty data)
- No build step, no framework dependency
- GitHub Pages hosting = free, global CDN
- Can progressively add React/SPA features without rewrite

### 3. Share via Native URI Schemes
**Decision:** Use `sms:` and `mailto:` URI schemes for sharing.

**Rationale:**
- Works on iOS and macOS without any API keys
- Opens native iMessage and Mail apps directly
- No server needed for sharing
- Fallback clipboard copy for other platforms

### 4. AI Translation Strategy
**Decision:** Use Claude API for translation with structured output.

**Future prompt strategy:**
- Input: raw menu text (Italian, French, etc.)
- Output: JSON with `{ name_original, name_english, description, ingredients[], category, dietary_flags[], cultural_notes }`
- Ingredient classification drives the emoji icon assignment
- Cultural context goes beyond literal translation

### 5. iOS App — SwiftUI + Vision
**Decision:** Native Swift app for Phase 4.

**Rationale:**
- Apple Vision framework for on-device OCR (no API call needed)
- CoreML for offline ingredient classification
- SwiftUI for modern, reactive UI
- Share Sheet integration for native iOS sharing
- Camera integration is first-class in Swift

## Data Model

```json
{
  "restaurant": {
    "name": "La Cipolla d'Oro",
    "location": { "city": "Ancona", "region": "Le Marche", "country": "IT" },
    "cuisine": "Italian — Marchigiano",
    "source_url": "https://www.leggimenu.it/menu/cipolladoro",
    "cover_charge": 2.50,
    "currency": "EUR"
  },
  "sections": [
    {
      "name_original": "Antipasti",
      "name_english": "Starters",
      "intro": "Sharing plates of local charcuterie...",
      "items": [
        {
          "name_original": "Degustazione di Salumi e Formaggi",
          "name_english": "Tasting board of cured meats & cheeses",
          "description": "A sharing platter of locally produced...",
          "price": 13.00,
          "ingredients": ["cured_meats", "cheese"],
          "dietary_flags": [],
          "cultural_notes": "Expect ciauscolo, a spreadable salame unique to Le Marche",
          "badges": ["great_for_sharing"]
        }
      ]
    }
  ]
}
```

## File Naming Convention

Menu HTML files: `menus/{restaurant-slug}.html`
Menu JSON data: `src/data/{restaurant-slug}.json`

Restaurant slug = kebab-case of restaurant name (e.g., `cipolla-doro`, `trattoria-da-mario`)
