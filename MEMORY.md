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
- Palette: Cream #F2E8D9, Gold #E8B86D, Rust #C4583B, Forest #2B4A3F, Espresso #1C1007, Sage #A8C5A0
- Fonts: Permanent Marker + DM Sans | Light mode only
- URL: https://marshallamoranto.github.io/space03-dev/projects/space03/gallery-70s.html

**Page structure:**
1. Sticky nav — Espresso bg, Gold border, Gold logo, Rust Resume CTA
2. Hero (90vh full-bleed) — random featured project, dot switcher, Ken Burns zoom, dark bottom gradient, frosted white pill labels ("Featured Work" + category), Gold CTA button
3. Page header + filter bar (All / Email / Digital Ads / Presentation / Production / Web Design)
4. Gallery grid — 5 cards, click opens lightbox
5. About section — Forest bg, two-column desktop / centered mobile, Cream/Gold text, Rust + ghost buttons
6. Footer — Espresso bg, Gold border, full-width

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

### Next Steps (when Marshall is ready)
1. Swap in real email + resume URL
2. Write real bio for About section
3. Decide on hero animation concept (TBD)
4. Decision: expand gallery-70s into full space03.com homepage?

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
