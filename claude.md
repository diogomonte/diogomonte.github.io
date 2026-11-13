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

- `index.html` — the entire homepage as a single page: hero, then `#focus`, `#portfolio` (labelled "Work"), `#writing`, `#about`, `#policies` sections, all anchor-linked from one nav (`.nav-links`). New projects/policies get a row added in the matching list (`.project-list` / `.policy-list`), linking out to a standalone detail page.
- Writing lives on Medium (https://medium.com/@diogomonte), not in this repo. The `#writing` section, hero CTA and footer link point there; there are no local article pages.
- `portfolio/*.html`, `policies/*.html` — standalone detail pages (one per project or app privacy policy). Each is a full independent HTML document, not a template/partial — copy an existing file in the same folder as a starting point to match structure and styling classes (`subpage-hero`, `prose-container`, `prose`).
- `styles.css` — single global stylesheet shared by every page (root + subfolders reference `styles.css` or `../styles.css`). Design tokens are CSS custom properties in `:root` at the top — reuse them rather than hardcoding values.
- `scripts.js` — minimal vanilla JS (mobile nav toggle, scroll-spy active-link highlighting via `IntersectionObserver`, smooth-scroll for in-page anchors).
- `images/` — static image assets referenced by relative path.

## Design system ("blueprint / systems")

- Tokens: `--paper` #F5F7FA, `--surface` #FFF, `--ink` #13233A, `--slate` #4B5A6E, `--rule` #D5DCE5, `--blueprint` #2F5BB7 (the only accent). Older `--color-*` names remain as aliases.
- Type: Source Serif 4 for h1/h2, the wordmark and the writing statement; IBM Plex Sans for everything else. Both loaded from Google Fonts in each page's `<head>`.
- The hero's blueprint grid is the one bold element. Elsewhere: hairline rules and whitespace, no shadows, no rounded cards, no uppercase eyebrow labels, no emoji in headings.
- Homepage sections use `.section-grid` (title in a narrow left column, content on the right; stacks below 900px).

## Content conventions

- Projects are `.project-row` items (title, description, stack); policies are `.policy-row` items with a "Privacy policy" link.
- Positioning: software architect focused on architecture, AI-assisted development and design. Keep copy plain and factual.
