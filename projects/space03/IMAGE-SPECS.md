# space03 — Image Asset Specs

## Hero Images (Featured Hero Section)

### Desktop Hero
- **Canvas:** 1600 × 900px (16:9)
- **Live/safe area:** center 1100 × 600px (key subject/focal point stays here)
- **Note:** Bottom ~35% is covered by dark gradient + text overlay — keep focal point in upper 60%
- **Format:** JPG
- **Target file size:** 200–350KB
- **Filename convention:** `[project]-hero.jpg` (e.g. `legalzoom-hero.jpg`)

### Mobile Hero
- **Canvas:** 800 × 1000px (~4:5 portrait)
- **Live/safe area:** center 640 × 800px
- **Note:** Displays full viewport width at ~90vh tall on phone — portrait crops are essential
- **Format:** JPG
- **Target file size:** 100–180KB
- **Filename convention:** `[project]-hero-mobile.jpg` (e.g. `legalzoom-hero-mobile.jpg`)

### Hero Asset Folder
Place all hero images in: `hero-images/`

---

## Gallery Thumbnail Images

Used in the portfolio grid cards (the `.card-thumb` area).

- **Canvas:** 600 × 400px (3:2 landscape)
- **Display size:** ~280–360px wide × 200px tall (CSS grid auto-fill)
- **Note:** Cards display at 200px height with `object-fit: cover` — a 3:2 crop ensures nothing important is cut off
- **Format:** JPG
- **Target file size:** 60–120KB
- **Filename convention:** `[project]-thumb.jpg` (e.g. `legalzoom-thumb.jpg`)

---

## Lightbox / Portfolio Images

Full-size project images shown in the lightbox.

- **Recommended max width:** 1400px on longest side
- **Format:** JPG (photos), PNG (UI/flat graphics)
- **Target file size:** 150–400KB per image
- **No strict crop ratio** — use whatever best presents the work

---

## Summary Table

| Asset          | Canvas         | Safe Area      | Format | Size target |
|----------------|----------------|----------------|--------|-------------|
| Hero desktop   | 1600 × 900px   | 1100 × 600px   | JPG    | 200–350KB   |
| Hero mobile    | 800 × 1000px   | 640 × 800px    | JPG    | 100–180KB   |
| Gallery thumb  | 600 × 400px    | —              | JPG    | 60–120KB    |
| Lightbox image | 1400px max     | —              | JPG/PNG| 150–400KB   |
