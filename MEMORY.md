# MEMORY.md - Long-Term Memory

## Identity / iMessage Setup

- **Kai's dedicated Apple ID:** marshall.agentkai@gmail.com
- **Status:** ✅ WORKING — Kai now responds from marshall.agentkai@gmail.com
- **macOS user:** "Kai AI Agent" (username: Kai) on Mac mini
- **Relay:** Python script `/Users/Kai/imsg-rpc-relay.py` — started via Login Item `/Users/Kai/start-relay.sh`
- **DB path:** `/Users/Kai/Library/Messages/chat.db` (was wrongly pointing at Marshall's DB — fixed 2026-03-14)
- **LaunchAgents:** All unloaded/disabled — Login Item is the correct approach
- **Wrapper:** `~/.openclaw/scripts/imsg-kai` proxies OpenClaw RPC through Unix socket `/tmp/kai-imsg-rpc.sock`
- **SSH key:** `~/.ssh/id_kai` (Marshall→Kai for relay management)
- **Note:** Relay MUST run as a Login Item (GUI session child), NOT a LaunchAgent. LaunchAgent context lacks Automation:Messages permission. Terminal.app has Messages permission and Login Items inherit it.

## space03.com Portfolio Redesign Project

### Status: In Progress (started 2026-04-30)
- **Old site:** www.space3001.com (WordPress, last updated Spring 2022)
- **New domain:** www.space03.com (replacing current WordPress template)
- **Approach:** Fresh HTML5/CSS — no WordPress
- **GitHub repo:** https://github.com/marshallamoranto/space03-dev
- **GitHub Pages:** https://marshallamoranto.github.io/space03-dev/

### Locked In
- **Font:** Fraunces Italic (headlines) + Satoshi (body)
- **Palette:** Warm Sunset — Amber #FF9A3C → Rose #FF4E8A → Plum #7B2FBE
- **Style:** Modern minimalist, youthful, subtle gradients, rounded edges

### Design Direction
- HTML5 animation in hero section (concept TBD — Marshall still deciding)
- Light vs dark background: both mocked up, Marshall still deciding
- Portfolio pieces porting from space3001.com (LZ, JD, BD, TD, webdesign categories)

### Files (workspace)
- `projects/space03/PROJECT.md` — project brief
- `projects/space03/styleguide.html` — v1 style guide (old palette/fonts)
- `projects/space03/explore.html` — font & palette explorer round 1
- `projects/space03/fonts2.html` — font explorer round 2 (11 more fonts)
- `projects/space03/styleguide-v2.html` — ✅ current style guide (Fraunces + Warm Sunset, light/dark toggle)

### GitHub Pages URLs
- Style guide v2: https://marshallamoranto.github.io/space03-dev/styleguide-v2.html
- Font explorer: https://marshallamoranto.github.io/space03-dev/fonts2.html

### Gallery Pages (built + iterated 2026-05-07)

#### gallery.html — Warm Sunset version
- Palette: Amber #FF9A3C → Rose #FF4E8A → Plum #7B2FBE | Fonts: Permanent Marker + Satoshi
- Dark mode with toggle
- URL: https://marshallamoranto.github.io/space03-dev/projects/space03/gallery.html

#### gallery-70s.html — 70s Record version (PRIMARY / most developed)
- Palette: Cream #F2E8D9, Rust #C4583B, Forest #2B4A3F, Espresso #1C1007, Sage #A8C5A0
- **Gold (#E8B86D) replaced with White (#FFFFFF) throughout** (2026-05-11)
- Fonts: Permanent Marker + DM Sans | Light mode only
- URL: https://marshallamoranto.github.io/space03-dev/projects/space03/gallery-70s.html
- **Live on server:** http://space03.com/new/gallery-70s.html (subfolder, WP still at root)

**Page structure:**
1. Sticky nav — Espresso bg, White border, White logo, Rust Resume CTA
2. Hero (90vh full-bleed) — random featured project, dot switcher, Ken Burns zoom, dark bottom gradient, White CTA button. "Featured Work" label REMOVED (2026-05-11)
3. Page header + filter bar (All / Email / Digital Ads / Presentation / Production / Web Design)
4. Gallery grid — 5 cards, click opens lightbox
5. About section — Forest bg, two-column desktop / centered mobile, Cream/White text, Rust + ghost buttons
6. Footer — Espresso bg, White border, full-width

**Lightbox:**
- Inner nav (‹ ›) flips images within a project; outer nav (← →) changes project + updates info panel
- Desktop: image left / info right | Mobile: stacked + Espresso "✕ Close" bar at bottom

**Real projects (images from space3001.com/popups/images/):**
- LegalZoom — Email Campaign — LZ6b, LZ5, LZ4, LZ3, LZ7, LZ8, LZ9
- Joe Digital — Digital Advertising — JD1–JD5
- Booz Digital — Presentation Design — BD1a–BD1d
- The Daily — Production Design — Ipad_UI_1–12
- Thoughthorse — Web Design — webdesign1a_updated, webdesign2, webdesign3

**Still needs (placeholders in file):**
- YOUR_EMAIL → marshall@space3001.com (or new address)
- YOUR_RESUME_URL → https://www.space3001.com/images/Resume.pdf (or updated PDF)
- Real bio text in About section

### Key Bug Fixes Applied (for reference)
- Active filter button: `border: none` on `.filter-btn.active` — border was causing dark edge artifact with gradient
- Lightbox ✕ close button: `align-items/justify-content: center` must stay inside `.lb-close` rule (CSS was malformed/orphaned)
- Footer: removed `max-width: 1100px` — now spans full width like the nav
- Top bar: White bar at very top of page with "The Portfolio of Marshall Amoranto" (above nav)
- Gradient text wash fix (2026-05-11): `.lb-title` and `.page-title` use hardcoded `linear-gradient(135deg, #C4583B 0%, #2B4A3F 100%)` — NOT `var(--grad)` which starts white and washes out on light bg

### Hero Image System (added 2026-05-11)
- Hero uses **separate dedicated images** from lightbox/portfolio images
- Each card has `data-hero-img` (desktop) and `data-hero-img-mobile` (mobile) attributes
- JS picks desktop vs mobile based on viewport width (breakpoint: 640px)
- Falls back to `data-img` (first portfolio image) if no hero image set yet
- Hero images live in `hero-images/` folder on server
- **Image specs saved to:** `projects/space03/IMAGE-SPECS.md`
  - Hero desktop: 1600×900px, safe area 1100×600px, JPG, 200–350KB
  - Hero mobile: 800×1000px, safe area 640×800px, JPG, 100–180KB
  - Gallery thumb: 600×400px, JPG, 60–120KB
  - Lightbox: 1400px max, JPG/PNG, 150–400KB
- **Filename convention:** `[project]-hero.jpg` / `[project]-hero-mobile.jpg`
  - legalzoom, joedigital, boozdigital, thedaily, thoughthorse

### FTP / Deployment (set up 2026-05-11)
- **FTP host:** 69.31.189.18 (space03.com resolves here)
- **Username:** space03
- **Remote web root:** `/public_html/` (WordPress still lives here)
- **Current staging path:** `/public_html/new/` → http://space03.com/new/gallery-70s.html
- **hero-images/ folder** created on server at `/public_html/new/hero-images/`
- **Desktop upload folder:** `~/Desktop/space03-upload/` — always kept in sync with latest HTML
- Kai can FTP upload directly using curl to 69.31.189.18
- When ready to go live at root: rename/disable WP `index.php`, promote `gallery-70s.html`

### Adding/Editing Portfolio Pieces
Each card is a `<div class="gallery-card">` block with these data attributes:
- `data-category` — filter category (email / digital / presentation / production / web)
- `data-img` — thumbnail / first image URL
- `data-images` — JSON array of all image URLs for that project
- `data-hero-img` / `data-hero-img-mobile` — dedicated hero background images
- `data-title`, `data-tag`, `data-desc`, `data-skills` — text content
- Kai can add/edit/remove cards and FTP directly to the server

### Next Steps (when Marshall is ready)
1. Create hero images (desktop + mobile) for each project per IMAGE-SPECS.md
2. Upload hero images → Kai can FTP them directly once files are ready
3. Swap in real email + resume URL (placeholders: YOUR_EMAIL, YOUR_RESUME_URL)
4. Write real bio for About section
5. Upload portfolio images to space03.com server and update src paths (currently hotlinked from space3001.com)
6. Go live at root — promote from /new/ to public_html/

## Investment Project
- **File:** `portfolio.md` — full holdings, contributions log, watch list
- **Goal:** $100,000 (currently at $37,629, +50.14% total gain)
- **Weekly adds:** ~$300/week
- **Ethics screen:** Hard NO on fossil fuels, animal testing, weapons
- **Theme:** Clean energy, AI, EVs, plant-based food
- **Kai's role:** Track adds, flag news on holdings, suggest weekly deployment targets
- **Watch:** BYND (holding on principle but underperforming), LOCL (solvency), SMCI (governance), SOUN (volatile)
- **Started:** 2026-04-10

## Pending Setup Tasks (do when Marshall is at Mac)
1. **Photo access** — grant read permissions to Kai's Messages attachments folder
2. **Google Drive** — connect Google account via `gog` skill

## System / Infrastructure

- **Gateway nightly SIGTERM (~11pm PST):** macOS kills and restarts the OpenClaw gateway as part of nightly scheduled maintenance. When it restarts, the iMessage provider picks up recent messages again. This is expected behavior, not a bug.

## Post-OS-Update iMessage Fix (2026-04-08)
After a macOS update, iMessage relay may break due to:
1. Execute bit stripped from `/Users/marshall/.openclaw/scripts/imsg-kai` → fix (as Marshall): `chmod +x /Users/marshall/.openclaw/scripts/imsg-kai`
2. Kai loses traverse access to Marshall's home dir and `.openclaw/` → fix (as Marshall):
   ```
   chmod +a "Kai allow execute,read" /Users/marshall
   chmod +a "Kai allow execute,read" /Users/marshall/.openclaw
   chmod +a "Kai allow execute,read" /Users/marshall/.openclaw/scripts
   ```
Full Disk Access for Terminal/imsg in System Settings is NOT enough alone — directory ACLs must also be set.
