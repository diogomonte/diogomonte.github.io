# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Diogo Monte's personal portfolio site: static HTML/CSS/vanilla-JS, deployed directly via GitHub Pages (no build step, no bundler, no package.json). Every page is served as-is from the repo root.

## Development

There is no build/lint/test tooling. To preview locally, just open `index.html` in a browser, or serve the directory:

```
python3 -m http.server 8000
```

There are no automated tests. Verify changes by opening the affected page(s) in a browser and checking layout/links manually.

## Architecture

- `index.html` — the entire homepage as a single-page app: hero, then `#portfolio`, `#articles`, `#policies`, `#about` sections, all anchor-linked from one nav (`.nav-links`). New portfolio/article/policy entries get a summary card added directly in the matching section of `index.html`, linking out to a standalone detail page.
- `portfolio/*.html`, `articles/*.html`, `policies/*.html` — standalone detail pages (one per project, blog post, or app privacy policy). Each is a full independent HTML document, not a template/partial — copy an existing file in the same folder as a starting point for a new one to match structure and styling classes.
- `styles.css` — single global stylesheet shared by every page (root + subfolders all reference `../styles.css` or `styles.css` depending on depth). Design tokens (colors, radii, shadows, fonts) are CSS custom properties in `:root` at the top — reuse these vars rather than hardcoding values.
- `scripts.js` — minimal vanilla JS included on `index.html` only, handling: mobile nav toggle, scroll-spy active-link highlighting via `IntersectionObserver`, and smooth-scroll for in-page anchor links.
- `images/` — static image assets referenced by relative path from wherever they're used.

## Design tokens (styles.css `:root`)

Color/spacing/shadow variables are already defined in `styles.css` (`--color-primary`, `--color-accent`, `--radius-md`, `--shadow-md`, etc.) — use these existing variables. Note the color palette in `styles.css` differs slightly from the one described later in this file's original prompt section (`--color-accent: #2563EB` vs `--accent: #2A9D8F`); treat `styles.css` as the source of truth since it's what's actually live on the site.

## Content conventions

- Cards (`.card`, `.project-card`, `.article-card`, `.policy-card`) follow a consistent `card-body` + `card-footer` structure — match this when adding entries.
- Article cards include a `tags` list and a `date` (e.g. `Dec 2025`) in `.card-meta`.
- Commented-out card markup in `index.html` (e.g. an unpublished article) is intentional — draft entries are left in place as HTML comments until ready to publish, not deleted.
