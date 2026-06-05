# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static HTML/CSS/JS personal portfolio site built on the [BootstrapMade "Personal" free template](https://bootstrapmade.com/personal-free-resume-bootstrap-template/) (Bootstrap v5.3.2). No build system, no package manager, no framework — all files are served as-is.

## Serving the site

Open `index.html` directly in a browser, or serve with any static file server:

```bash
# Python
python3 -m http.server 8080

# PHP
php -S localhost:8080
```

On this server the site is deployed at `/var/www/portfolio`, served by Apache/Nginx.

## Architecture

### Page structure

- `index.html` — single-page app with six anchor-linked sections: `#about`, `#resume`, `#services`, `#portfolio`, `#contact`
- `*-details.html` — one file per portfolio project, loaded as GLightbox overlays (not navigated to directly)

### How navigation works

`assets/js/main.js` drives the SPA behavior: clicking a nav link adds `header-top` to `#header` (collapses it), removes `section-show` from all sections, then adds `section-show` to the target section. Sections are hidden by default; the `section-show` class reveals them. The header starts expanded and only collapses once a section other than `#header` is selected.

### Portfolio filtering

Portfolio items use CSS filter classes: `filter-app` (Elementor), `filter-card` (Custom Code), `filter-web` (PHP/Backend). The Isotope library reads `data-filter` attributes on the `#portfolio-flters` `<li>` elements and shows/hides `.portfolio-item` elements accordingly.

### Vendor libraries (all local, no CDN except Google Fonts)

| Library | Purpose |
|---|---|
| Bootstrap 5.3.2 | Grid, utilities |
| GLightbox | Portfolio detail overlays (`data-glightbox="type: external"`) |
| Isotope | Portfolio grid filtering |
| Swiper | Image sliders in detail pages |
| Waypoints | Triggers skill bar animation on scroll |
| PureCounter | Animated counters |
| Boxicons / Bootstrap Icons / RemixIcon | Icon sets |

### Styling

`assets/css/style.css` is the only stylesheet to edit — the SCSS source is not included in this free template. The site uses a dark theme (`background: #000`) with green accent (`#18d26e`).

### Contact form

`forms/contact.php` is a non-functional stub (PHP/AJAX form requires the pro template version). The `<form>` in `index.html` is commented out.

## Adding a new portfolio project

1. Add a thumbnail image to `assets/img/portfolio/`
2. Add a `.portfolio-item` block in `index.html` inside `.portfolio-container` with the appropriate filter class (`filter-app`, `filter-card`, or `filter-web`)
3. Create a `projectname-details.html` by copying an existing detail file and updating its content — the Swiper slider, project info sidebar, and description
4. The detail page is opened as a GLightbox overlay via `data-glightbox="type: external"` on the anchor with class `portfolio-details-lightbox`
