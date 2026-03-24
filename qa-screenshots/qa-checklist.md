# QA Report: Carolina Corzo Martinez

**Date:** 2026-03-24
**URL:** https://cofoundy.github.io/portfolio-carolina-corzo/
**Status:** FAIL

## Data Validation
- [x] Name matches source (Carolina Corzo Martinez -- config.ts + Google Sheet)
- [x] Email matches source (c.corzom@hotmail.com -- config.ts + Sheet)
- [x] Title matches source (Gerente A&R | Desarrollo Artistico & Estrategia de Repertorio)
- [x] Stats match source (450+ canciones, 200+ lanzamientos, 350+ contratos)
- [x] All 6 credits present and match config.ts (Libertad, Ofrenda, Ocho, Inesperado Tour, MTV Unplugged, Y El Mundo No Se Acabo)
- [x] All 5 companies match config.ts (Universal Music, OCESA Seitrack, Cosmos Producciones, Samanez, HTA Management)
- [x] Education matches (MBA UNIR Mexico, UPC Peru)
- [x] Social links match (LinkedIn, Instagram, Muso Credits, Spotify, Email)
- [x] No hallucinated data detected

## Clean Deploy
- [x] No third-party watermarks (only Cofoundy credit at 0.2 opacity -- acceptable)
- [x] No placeholder text (no Lorem ipsum, no template defaults)
- [x] No template links (no "View on GitHub", "Fork this", etc.)
- [x] No "undefined" or visible "null" in content
- [x] No broken link text (no "#" or "javascript:void" visible)

## Technical
- [x] CSS loads (HTTP 200) -- _astro/index.esqHKtU6.css
- [x] Favicon file exists (HTTP 200 at /portfolio-carolina-corzo/favicon.svg)
- [ ] **ISSUE: Favicon href broken in HTML** -- renders as `/portfolio-carolina-corzofavicon.svg` (missing slash), returns HTTP 404
- [x] Google Fonts loaded (Bebas Neue, Inter, Space Grotesk)
- [x] Spotify embed iframe present with correct playlist URL
- [x] All 6 sections present: hero, creditos, trayectoria, playlist, sobre-mi, contacto
- [x] No profile image referenced (by design -- text-based hero for music industry)

## Mobile Responsiveness
- [ ] **ISSUE: Text overflow at 375px** -- Hero subtitle "GERENTE A&R | DESARROLLO ARTISTICO & ESTRATEGIA DE REPERTORIO" clips on the right edge
- [ ] **ISSUE: Stats row overflow at 375px** -- "200+" and "LANZAMIENTOS GESTIONADOS" text truncated/clipped on right side
- [x] overflow-x: hidden is set on html/body (prevents horizontal scrollbar but content still visually clips)
- [x] Mobile hamburger menu present

## Issues Found

### 1. FAVICON PATH BUG (Medium)
- **Location:** `src/pages/index.astro` line 16
- **Problem:** `href={import.meta.env.BASE_URL}favicon.svg` produces `/portfolio-carolina-corzofavicon.svg` (missing slash between base and filename)
- **Fix:** Change to `href={import.meta.env.BASE_URL + '/favicon.svg'}` or ensure BASE_URL ends with `/`
- **Impact:** Browser cannot find favicon; tab shows default icon

### 2. MOBILE TEXT OVERFLOW (Medium)
- **Location:** Hero section subtitle and stats row
- **Problem:** At 375px viewport, the subtitle with `tracking-[0.3em]` and the stats flex row exceed container width, causing text to clip beyond the right edge
- **Fix:** Reduce letter-spacing on mobile (`tracking-normal sm:tracking-[0.3em]`), or reduce font size further, or allow the subtitle to wrap. For stats, ensure `flex-wrap` works properly at small sizes.
- **Impact:** Content not fully readable on narrow mobile devices

## Evidence
- qa-desktop.png (1280x4000 viewport, full page)
- qa-mobile.png (375x812 viewport, above the fold)
