# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static website for **Objectif Maths Tours** — a private math tutoring business in Tours, France. Hosted on GitHub Pages at `objectif-maths-tours.fr` (see `CNAME`). No build tools, no framework, no dependencies to install.

## Local preview

Open `index.html` directly in a browser, or serve with any static server:

```bash
python -m http.server 8080
# then visit http://localhost:8080
```

The CSS is referenced with a cache-busting version query (`style.css?v=61`). When making significant CSS changes, increment that version number in the `<link>` tag in `index.html`.

## File structure and purpose

| File | Role |
|------|------|
| `index.html` | Main production page — single-page site with anchor navigation |
| `indexClaude.html` | Alternative design draft (self-contained with inline CSS; not linked from index) |
| `merci.html` | Post-form confirmation page; auto-redirects to home after 10 s |
| `style.css` | All styles for `index.html` and `merci.html` |
| `Revisions/fiches_revision_STI2D.html` | Standalone revision-sheet page for STI2D students; fully self-contained with inline CSS |
| `assets/` | Images only (logos, avatar, favicons, OG image) |
| `sitemap.xml` | Lists `index.html` and `merci.html` |

## Architecture notes

**Single-page layout.** `index.html` is one long page with sections navigated by anchor links: `#accueil → #services → #zone → #niveaux → #apropos → #methode → #tarifs → FAQ → #contact → #confidentialite → #mentions-legales`. The fixed navbar links to these anchors; `scroll-padding-top: 110px` offsets the fixed nav height.

**CSS design tokens.** All colours are CSS custom properties at the top of `style.css`:
- `--primary-blue: #143e63` / `--dark-navy: #0d2d4a`
- `--accent-orange: #e67e22`
- `--light-cream: #fafaf8`, `--soft-gray: #e8e8e4`, `--white: #ffffff`
- `--text-dark: #2a2a2a`, `--text-medium: #5a5a5a`

Typography: headings use **Cormorant Garamond** (serif), body uses **Jost** (sans-serif), both loaded from Google Fonts.

**Contact form.** Handled by [Formspree](https://formspree.io/) (`action="https://formspree.io/f/xojnjnre"`). On success it redirects to `merci.html` via a hidden `_next` field. A honeypot field (`name="_gotcha"`) provides basic spam protection.

**`indexClaude.html`** is a design alternative with its own inline CSS and different fonts (DM Sans + DM Serif Display). It is not linked anywhere and is not deployed. It can be used as a reference or to replace `index.html` if a redesign is chosen.

**`Revisions/fiches_revision_STI2D.html`** is a dark-themed, self-contained standalone page (no shared CSS) for STI2D Physique-Chimie & Maths revision sheets. It is not linked from the main site nav.

## SEO / metadata

- Schema.org `LocalBusiness` JSON-LD is embedded in `<head>` of `index.html`.
- Open Graph and Twitter card meta tags are present.
- Canonical URL: `https://objectif-maths-tours.fr/`.
- Update `sitemap.xml` `<lastmod>` dates when publishing significant content changes.
