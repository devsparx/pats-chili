# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page, fan-made tribute site for Pat's Chili Dogs (a.k.a. Pat's Drive In), a real restaurant at 1202 W Niagara St, Tucson AZ. Static, dependency-free: `index.html` + `style.css` and nothing else. No build step, no package manager, no tests, no framework.

## Running it

Open `index.html` directly in a browser, or serve the directory:

```
python3 -m http.server 8000 --directory /home/matthew/Dev/portfolio/pats-chili
```

Editing HTML/CSS requires only a browser reload. Google Fonts and the Google Maps embed are loaded from the network, so a fully offline preview will lose the display typefaces and the map.

## Structure and conventions

- **All markup lives in `index.html`**, in section order: nav → hero → `#history` → `#menu` → `#location` → footer. Nav anchors point at those section IDs; renaming an ID means updating `.nav-links` too.
- **JS is a ~15-line inline `<script>` at the bottom of `index.html`** — sticky-nav class toggle on scroll, plus smooth-scroll anchor handling that also closes the mobile drawer. The mobile menu toggle itself is an inline `onclick` on the `.nav-toggle` button. Keep new behavior in this inline script; do not introduce a JS file or bundler for small additions.
- **`style.css` is one file organized by banner comments** (`/* ---- NAV ---- */`, HERO, SECTIONS, HISTORY, MENU, LOCATION, FOOTER, RESPONSIVE). Add rules under the matching banner, not at the end of the file.
- **Colors and radii come from `:root` custom properties** (`--red`, `--red-dark`, `--yellow`, `--cream`, `--brown`, `--text`, `--bg`, `--shadow-*`, `--radius`). Use the variables; do not hardcode new hex values.
- **Three display fonts, each with a fixed role**: `Bowlby One SC` for headings/section titles/menu category titles, `Permanent Marker` for the logo wordmark, `Inter` for body text. New type should reuse one of the three; adding a font means editing the Google Fonts `<link>` in `<head>`.
- **Responsive is a single `@media (max-width: 768px)` block** at the bottom of `style.css` that collapses every multi-column grid to `1fr` and turns the nav into an off-canvas drawer (`.nav-links.open`). Any new grid needs a corresponding collapse rule there.
- **Menu items follow a fixed markup shape**: `.menu-item` → `.menu-item-header` containing `.menu-item-name`, an empty `.menu-item-dots` spacer (the dotted leader is a CSS border on that flex-filling span), and `.menu-item-price`; optional `.menu-item-desc` and `.badge` follow. Add `.featured` for the highlighted-item treatment. Unknown prices use `&mdash;`.

## Content accuracy

The site states real business facts — prices, hours, phone number, and the Patterson/Hernandez ownership history. The footer carries a disclaimer that this is unofficial and that prices/hours may be stale. Do not invent menu items, prices, hours, or history details; leave a price as `&mdash;` rather than guessing, and keep the disclaimer intact.
