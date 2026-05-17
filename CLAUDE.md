# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the static website for **Mande Films** — a husband-and-wife filmmaking team. There is no build system, no package manager, and no test suite. All pages are self-contained HTML files with inline CSS and JS.

## Development

Open any `.html` file directly in a browser, or serve locally:

```bash
python3 -m http.server 8000
```

There is no linting, no compilation step, and no deployment pipeline in this repository.

## Architecture

The site consists of individual HTML pages, each fully self-contained (styles and scripts inlined):

- `index.html` — Home page with hero video, stats, impact carousel, testimonials
- `about.html` — Team story and bios
- `portfolio.html` — Video portfolio grid with featured player
- `production.html` — Production services
- `contact.html` — Contact form
- `mxemedia-production.html` — MxE Media production page
- `ai-workflow-audit/index.html` — Separate AI workflow audit page

Assets live at the repository root: video (`Safari_for_website.mp4`), images (`ME_Final_Logo_White_Transparentsmall.png`, `Photo (1).jpg`–`Photo (27).jpg`, etc.), award laurels (`awards/`), and PDFs.

## Design System

All pages share identical CSS custom properties (dark theme — note the inverted naming convention):

```css
--white: #060b12       /* actual darkest background */
--off-white: #0a0f16
--light-grey: #0d1219
--charcoal: #141a24
--black: #ffffff       /* actual white text */
--amber: #7a9bbf       /* blue-grey accent */
```

Fonts: `Cormorant Garamond` (display/headings) and `Outfit` (body/UI), both from Google Fonts.

## Nav Logo

All pages except `index.html` use the image logo:

```html
<a href="/"><img src="ME_Final_Logo_White_Transparentsmall.png" alt="Mande Films" class="nav-logo-img"/></a>
```

The `index.html` originally used a text-only `<a class="nav-logo">` — if restoring or referencing the old style, note the CSS class difference (`nav-logo` vs `nav-logo-img`).

## Key Patterns

- **Scroll animations**: `.fade-up` elements get `.will-animate` added by JS on load, then `.visible` via `IntersectionObserver`.
- **Stats counter**: `.stat-number` elements use `data-target`, `data-prefix`, `data-suffix`, `data-millions` attributes; animated on scroll into view.
- **Impact carousel**: manually implemented with `translateX` on `#carouselTrack`; auto-advances every 5s when in viewport.
- **Awards slideshow**: auto-advancing with a clone of the first slide appended for seamless loop.
- **Video embeds**: thumbnail + play button; clicking sets the `iframe` `src` to a YouTube embed URL with `?autoplay=1`.
