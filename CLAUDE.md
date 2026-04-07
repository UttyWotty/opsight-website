# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for **OpSight Intelligence** (opsightintel.com), hosted on GitHub Pages with Cloudflare DNS. Three business verticals:

- **Fraud Intelligence** (`intelligence.html`): fraud ecosystem monitoring for financial institutions (vishing networks, mule accounts, image OCR, REST API, evidence-grade reporting). 2 core markets (Korea, Turkey) plus custom client pipelines.
- **Manufacturing Intelligence** (`manufacturing.html`): operational visibility for auto parts suppliers/OEMs (OEE dashboards, cycle time analysis)
- **AgentGuard** (`agentguard.html`): AI coding assistant security guardrails. Three-layer enforcement, 157 tests, ISO 27001/EU AI Act/Korean AI Basic Act compliance. Free + Team ($15/dev/mo) + Business ($25/dev/mo) tiers.

## Architecture

- **No build system, no framework** — plain HTML/CSS/JS served directly via GitHub Pages
- All styling is inline `<style>` blocks within each HTML file (no external CSS)
- `stats.json` — live stats (entities, clusters, members, markets) fetched by `intelligence.html` to display dynamic counters
- `demodashboard/` — standalone demo dashboard pages (capacity, cycle time efficiency, run rate) for the manufacturing vertical
- `CNAME` — points to `opsightintel.com`

## Development

No build, lint, or test commands. To preview locally, serve the directory with any static file server:

```
python3 -m http.server 8000
```

## Multi-language Support

`intelligence.html` supports English (`en`), Korean (`ko`), and Turkish (`tr`) via `data-lang` attributes toggled by switching `html[lang]`. Content for all languages lives in the same HTML file with CSS-driven visibility.

`manufacturing.html` and `agentguard.html` are English-only. `index.html` is the homepage linking to all three verticals.
