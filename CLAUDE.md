# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-page static website for **International Barbers**, a barbershop at 126 Ashley Road, St Paul's, Bristol BS6 5PA. Phone: 07447 980180.

## Architecture

Everything lives in one file: `index.html` (~1,300 lines). All CSS is in an inline `<style>` tag, all JS in an inline `<script>` tag. No build tools, no frameworks, no package.json.

- **CSS**: Mobile-first with custom properties in `:root`. Breakpoints at 640px (tablet), 768px (desktop nav), 1024px (wide). Design system uses charcoal (#1a1a1a), gold (#c8a45c), cream (#f5f2ed).
- **Fonts**: Google Fonts — Cinzel (headings, matches the shop sign) + DM Sans (body).
- **JS**: Vanilla only. Handles mobile nav toggle, scroll-based nav background, IntersectionObserver fade-in animations, today's hours highlighting, and contact strip hours population.

## Assets

- `frontOfHouse.png` — Google Maps screenshot of the storefront (used in About section)
- `font_picture.png` — Photo of the shop sign (font reference, not displayed on site)
- `headshots/` — 7 photos: 1 interior shop shot (used as hero background), 6 haircut close-ups (used in gallery)
- Image filenames contain spaces — use as-is in HTML `src`, browsers handle them fine

## Running Locally

```
npx serve -l 8080
```

Python is not installed on this machine. No install step needed.

## Deployment

Static site, deploy-ready on Vercel/Netlify. The directory structure (index.html + images at same level) must be preserved.

## Git

- **Repo**: https://github.com/zackraven/internationalBarbers
- **Branch**: main
- **Commit identity**: Use `zackraven` / `alexcolumbojordansmith@gmail.com` for all commits on this repo (set via local git config)

## Sections (DOM order)

`nav` → `#hero` → contact strip → `#about` → `#services` → `#gallery` → `#hours` → `#find-us` → mobile call button → `footer`

## Key Implementation Details

- Hero uses CSS `background-image` with a gradient overlay div, not an `<img>` tag
- Mobile nav is a slide-in panel from the right with an overlay backdrop
- A floating gold call button is fixed bottom-right on mobile (hidden at 768px+)
- Opening hours rows use `data-day` attributes (0=Sunday, 1=Monday, etc.) matched against `new Date().getDay()`
- Google Maps embed uses a search query URL (no API key required)
- All below-fold images use `loading="lazy"`
