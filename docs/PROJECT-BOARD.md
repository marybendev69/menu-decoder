# Project Board — GitHub Issues to Create

These issues should be added to the **Menu Decoder** GitHub Project board.
Create them as issues in the `menu-decoder` repo and link to the project.

---

## Phase 1: Foundation (MVP — GitHub Pages)

### Issue 1: Deploy to GitHub Pages
**Labels:** `infra`, `priority:high`
**Status:** Todo

Create the `menu-decoder` repo, push initial files, enable GitHub Pages on `main` branch. Verify the landing page and Cipolla d'Oro menu load at `aguidice.github.io/menu-decoder`.

**Acceptance criteria:**
- [ ] Repo created at github.com/Aguidice/menu-decoder
- [ ] GitHub Pages enabled (Settings → Pages → main branch)
- [ ] Landing page loads at aguidice.github.io/menu-decoder
- [ ] Menu loads at aguidice.github.io/menu-decoder/menus/cipolla-doro.html
- [ ] All emoji icons render correctly on mobile Safari

---

### Issue 2: Add dietary filter toggles
**Labels:** `feature`, `phase-1`
**Status:** Todo

Add toggle buttons above the menu that filter dishes by dietary category. When "Vegetarian" is toggled, only 🌿 dishes show. When "Fish" is toggled, only 🐟 dishes show. Multiple filters = OR logic (show anything matching any active filter).

**Acceptance criteria:**
- [ ] Filter bar with toggle buttons for each ingredient category
- [ ] Dishes that don't match active filters are dimmed or hidden
- [ ] Filters work alongside the tap-to-select ordering system
- [ ] Clear all button resets filters

---

### Issue 3: Add "back to top" and section quick-jump
**Labels:** `ux`, `phase-1`
**Status:** Todo

On mobile, the sticky nav is hard to use with many sections. Add a floating "back to top" button and a collapsible section picker overlay.

---

### Issue 4: Responsive polish for mobile Safari
**Labels:** `bug`, `ux`, `phase-1`
**Status:** Todo

Test on iPhone Safari, Android Chrome, iPad. Fix any layout issues with the share bar, nav overflow, or emoji rendering. Ensure `sms:` and `mailto:` links work correctly on iOS.

---

## Phase 2: URL Ingestion

### Issue 5: Build menu scraper for leggimenu.it
**Labels:** `feature`, `phase-2`
**Status:** Backlog

Create a Node.js or Python script that takes a leggimenu.it URL, scrapes all section pages, and outputs structured JSON matching the data model in ARCHITECTURE.md.

**Acceptance criteria:**
- [ ] Script accepts a base URL (e.g., `leggimenu.it/menu/cipolladoro`)
- [ ] Discovers all section links automatically
- [ ] Outputs JSON with sections, items, prices
- [ ] Handles Italian special characters correctly

---

### Issue 6: AI translation pipeline (Claude API)
**Labels:** `feature`, `ai`, `phase-2`
**Status:** Backlog

Build a pipeline that takes scraped menu JSON (Italian) and sends it to the Claude API for translation, ingredient classification, and cultural context generation. Output enriched JSON matching the data model.

**Acceptance criteria:**
- [ ] Takes raw menu JSON as input
- [ ] Calls Claude API with structured output prompt
- [ ] Returns enriched JSON with translations, descriptions, ingredient tags, dietary flags
- [ ] Handles batch processing (multiple sections in one call)
- [ ] Cost-efficient prompt design (minimize tokens)

---

### Issue 7: HTML template generator
**Labels:** `feature`, `phase-2`
**Status:** Backlog

Build a script that takes enriched menu JSON and generates a styled HTML page matching the Cipolla d'Oro design. Parameterize restaurant name, colors, and content.

**Acceptance criteria:**
- [ ] Takes enriched JSON → outputs complete HTML file
- [ ] Includes all emoji icons, sharing JS, and responsive CSS
- [ ] Restaurant name, location, and color scheme are configurable
- [ ] Output can be dropped into `menus/` and served immediately

---

### Issue 8: "Paste a URL" input on landing page
**Labels:** `feature`, `ux`, `phase-2`
**Status:** Backlog

Add a URL input field to the landing page. User pastes a digital menu URL → triggers scrape + translate pipeline → generates and displays the decoded menu.

---

## Phase 3: Photo to Menu

### Issue 9: Camera capture + OCR (web)
**Labels:** `feature`, `phase-3`
**Status:** Backlog

Add camera capture to the web app using the MediaDevices API. Process captured image with Tesseract.js for OCR text extraction. Feed extracted text into the AI translation pipeline.

---

### Issue 10: Camera capture + OCR (iOS — Vision framework)
**Labels:** `feature`, `ios`, `phase-3`
**Status:** Backlog

Build iOS camera integration using SwiftUI + Apple Vision framework for on-device OCR. No API call needed for text extraction.

---

## Phase 4: iOS App

### Issue 11: iOS app scaffold (SwiftUI)
**Labels:** `feature`, `ios`, `phase-4`
**Status:** Backlog

Create the Xcode project with SwiftUI. Tab bar with: Camera, My Menus (saved), Browse. Basic navigation and data model.

---

### Issue 12: Offline menu caching
**Labels:** `feature`, `ios`, `phase-4`
**Status:** Backlog

Cache decoded menus locally on-device so they work without internet. Important for travelers with limited data.

---

### Issue 13: Share Sheet integration
**Labels:** `feature`, `ios`, `phase-4`
**Status:** Backlog

Native iOS Share Sheet for sharing order lists via Messages, Mail, WhatsApp, AirDrop, etc.

---

## Phase 5: Multi-Language

### Issue 14: Multi-language support
**Labels:** `feature`, `phase-5`
**Status:** Backlog

Support any source language → any target language. Detect source language automatically. Let user choose their preferred output language.

Priority languages: French, Japanese, Thai, Spanish, Greek, Portuguese, German, Chinese, Korean, Arabic.

---

### Issue 15: Crowdsourced menu database
**Labels:** `feature`, `community`, `phase-5`
**Status:** Backlog

Allow users to submit decoded menus to a shared database. Other travelers can search by restaurant name or location and find pre-decoded menus.
