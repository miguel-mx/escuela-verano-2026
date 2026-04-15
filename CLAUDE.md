# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

A static single-page website for the **XXV Escuela de Verano en Matemáticas 2026** — a one-week summer math school hosted by the Centro de Ciencias Matemáticas (CCM), UNAM Campus Morelia. There is no build step, no package manager, and no server-side code.

## Development

Open `index.html` directly in a browser, or use any static file server:

```bash
python -m http.server 8080
# or
npx serve .
```

There are no linters, tests, or CI configured.

## Architecture

The entire site is a single `index.html` with one custom stylesheet `css/esver.css`. All interactivity is vanilla JavaScript inline at the bottom of `index.html`.

**External dependencies (CDN only):**
- Bootstrap 5.3.2 (CSS + JS bundle)
- Bootstrap Icons 1.11.3
- Google Fonts — Montserrat

**CSS design tokens** (defined in `:root` in `esver.css`):
- `--main-ev-color: #000AFF` — primary blue used for highlights, active states, timeline lines
- `--main-bg-color: #1D1D1B` — dark background
- `--gray-color: #9F9F9F`

**Page sections** (in order, each with an `id`):
1. `.hero-image` — full-bleed banner (mobile: `banner-mobile.png`, desktop: `banner-header.png` via media query)
2. `#infographic` — key dates strip
3. `#intro` — description and registration CTA
4. `#registro` — registration steps and insurance download
5. `#cursos-platicas` — two-column grid of courses (C1–C6) and talks (P1–P3)
6. `#program` — tabbed daily schedule (Monday–Friday) with a CSS timeline layout
7. Gallery — 7 photos in a two-row Bootstrap grid
8. `#pccm` — PCCM graduate program promotion section
9. `#footer` — social links, contact email, organizers, copyright

**Schedule tab JS** (bottom of `index.html`): On `DOMContentLoaded`, maps `today.getDay()` to a tab index and auto-activates the matching day tab. Note: the tab elements use `id="lunes-tab"` etc. via Bootstrap `data-bs-toggle="pill"`, but the JS uses `id="tab-0"` etc. which don't exist in the current markup — this auto-select logic is currently broken.

**Responsive behavior:** The navbar overlays the hero transparently on `≥768px` (`.custom-navbar` uses `position: absolute`). Below that breakpoint the navbar is static and the hero uses a mobile banner. Gallery heights and typography scale via the `@media (min-width: 768px)` block in `esver.css`.

**Registration system** links point to `https://tic.matmor.unam.mx/esver26/registro/new` (external app, not part of this repo).
