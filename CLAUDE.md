# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML website for **AxisLayer Exteriors**, an Edmonton, Alberta-based exterior contractor. No build process — all files are plain HTML/CSS/JS served directly via Vercel.

## Deployment

- **Platform**: Vercel (configured in `vercel.json`)
- **Redirects**: www → non-www, HTTP → HTTPS
- **Cache**: `/assets/` served with 1-year immutable cache headers
- No build step, no `npm install`, no compilation needed

## Architecture

### Directory Layout

- `index.html` — Homepage
- `services/{service-slug}/index.html` — Main service pages
- `{topic-slug}/index.html` — Supporting SEO pages (e.g., `parging-cost-edmonton/`)
- `projects/{project-slug}/index.html` — Portfolio case studies
- `blog/{post-slug}/index.html` — Blog articles
- `about/`, `contact/` — Static info pages
- `template/` — HTML templates with `[TEMPLATE]` placeholder markers for new pages
- `assets/css/main.css` — All custom styles
- `assets/js/main.js` — Vanilla JS interactions
- `assets/vendor/` — Third-party libraries (Bootstrap 5, AOS, GLightbox, Swiper, Isotope, PureCounter, FontAwesome)
- `sitemap.xml`, `sitemap-*.xml` — Multiple sitemaps split by content type

### Page Structure Convention

Every page follows this consistent layout:
1. `<head>`: meta tags, Open Graph, canonical URL, preloads, CSS/fonts
2. Schema.org JSON-LD blocks (always includes `LocalBusiness`; add `Service`, `BlogPosting`, `FAQPage`, `ConstructionProject` as appropriate)
3. `<header>`: nav with dropdowns (Services, Projects, Blog, Contact)
4. Hero section (Swiper carousel or static banner) with CTA buttons
5. Content sections
6. Footer with business info and service area
7. WhatsApp float button
8. Vendor JS (deferred) + `main.js`

### SEO Patterns

- Every page has a unique `<title>`, `<meta name="description">` (150–160 chars), and `<link rel="canonical">`
- `LocalBusiness` schema on every page; content-specific schemas layered on top
- `BlogPosting` + `FAQPage` schemas on blog posts
- `ConstructionProject` schema on project pages
- `Service` schema on service pages
- Sitemaps must be updated when adding new pages (see existing sitemap files for format)

### Forms

- Contact forms use **Formspree** endpoint: `https://formspree.io/f/mvzdbqvo`

### Images

- Use `.webp` format; include `loading="lazy"` on non-hero images
- Hero/above-fold images use `<link rel="preload">` in `<head>`

## Creating New Pages

1. Copy the closest existing page or use `template/` as a starting point
2. Replace all `[TEMPLATE]` markers and update all meta tags, canonical URL, and schema JSON-LD
3. Add the new URL to the appropriate `sitemap-*.xml` file
4. Link to it from relevant existing pages (service pages, nav, footer as appropriate)
