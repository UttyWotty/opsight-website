# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for **OpSight Intelligence** (opsightintel.com), hosted on GitHub Pages with Cloudflare DNS. Two business verticals:

- **Fraud Intelligence** — main site (`index.html`): fraud ecosystem monitoring for financial institutions (vishing networks, mule accounts, evidence-grade reporting)
- **Manufacturing Intelligence** (`manufacturing.html`): operational visibility for auto parts suppliers/OEMs (OEE dashboards, cycle time analysis)

## Architecture

- **No build system, no framework** — plain HTML/CSS/JS served directly via GitHub Pages
- All styling is inline `<style>` blocks within each HTML file (no external CSS)
- `stats.json` — live stats (entities, clusters, members, markets) fetched by `index.html` to display dynamic counters
- `demodashboard/` — standalone demo dashboard pages (capacity, cycle time efficiency, run rate) for the manufacturing vertical
- `CNAME` — points to `opsightintel.com`

## Development

No build, lint, or test commands. To preview locally, serve the directory with any static file server:

```
python3 -m http.server 8000
```

## Multi-language Support

`index.html` supports English (`en`), Korean (`ko`), and Turkish (`tr`) via `data-lang` attributes toggled by switching `html[lang]`. Content for all languages lives in the same HTML file with CSS-driven visibility.

`manufacturing.html` is English-only.
