# OpSight Intel — Website Visibility Fix Checklist

Your site works at `yourusername.github.io/reponame` but returns 403 via `opsightintel.com`. The problem is Cloudflare blocking non-browser requests, which means Google, search engines, social media previews, and all bots are blocked. Your site is invisible to the internet.

---

## Priority 1: Fix Cloudflare (Do This First)

Everything else is pointless until this is fixed.

- [ ] Log in to Cloudflare dashboard (dash.cloudflare.com)
- [ ] Select the opsightintel.com zone
- [ ] Go to **Security > Bots** — turn OFF "Bot Fight Mode"
- [ ] Go to **Security > Settings** — set Security Level to "Essentially Off" or "Low"
- [ ] Go to **Security > Settings** — turn OFF "Browser Integrity Check" if it's on
- [ ] Go to **Rules > Configuration Rules** — check if there are any rules blocking traffic, delete any that block bots or require challenges
- [ ] **Test:** After saving, wait 2 minutes, then try opening `https://opsightintel.com` in a private/incognito window. Also ask a friend to try from a different network.

### How to verify the fix worked

Open your terminal and run:

```bash
curl -I https://opsightintel.com
```

You should see `HTTP/2 200` (not 403). If you still see 403, something in Cloudflare is still blocking.

---

## Priority 2: Add robots.txt (Tells Search Engines They Can Crawl)

Create a file called `robots.txt` in the root of your GitHub Pages repo with this content:

```
User-agent: *
Allow: /

Sitemap: https://opsightintel.com/sitemap.xml
```

Commit and push it.

---

## Priority 3: Add sitemap.xml (Tells Search Engines Which Pages Exist)

Create a file called `sitemap.xml` in the root of your repo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://opsightintel.com/</loc>
    <lastmod>2026-04-03</lastmod>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://opsightintel.com/intelligence</loc>
    <lastmod>2026-04-03</lastmod>
    <priority>0.9</priority>
  </url>
  <url>
    <loc>https://opsightintel.com/manufacturing</loc>
    <lastmod>2026-04-03</lastmod>
    <priority>0.9</priority>
  </url>
</urlset>
```

Adjust the URLs to match your actual page paths. If your pages are at different paths (like `/index.html#intelligence`), use those instead. Add the OpSentry page when you create it.

Commit and push it.

---

## Priority 4: Add Meta Tags to Your HTML (Better Search Results and Social Previews)

Add these tags inside the `<head>` section of each HTML page.

### For the main/intelligence page:

```html
<!-- SEO -->
<meta name="description" content="Fraud ecosystem intelligence for financial institutions. Continuous monitoring of vishing networks, financial flow mapping, and evidence-grade reporting.">
<meta name="keywords" content="fraud intelligence, vishing, telegram monitoring, financial crime, OSINT, threat intelligence">
<meta name="author" content="OpSight Intelligence">

<!-- Open Graph (Facebook, LinkedIn link previews) -->
<meta property="og:title" content="OpSight Intelligence — Fraud Ecosystem Intelligence">
<meta property="og:description" content="Continuous monitoring of fraud infrastructure so you can act before losses occur.">
<meta property="og:url" content="https://opsightintel.com/">
<meta property="og:type" content="website">
<meta property="og:image" content="https://opsightintel.com/og-image.png">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="OpSight Intelligence — Fraud Ecosystem Intelligence">
<meta name="twitter:description" content="Continuous monitoring of fraud infrastructure so you can act before losses occur.">
<meta name="twitter:image" content="https://opsightintel.com/og-image.png">
```

### For the manufacturing page:

```html
<meta name="description" content="Operational visibility for auto parts suppliers and OEMs. OEE dashboards, cycle time analysis, and custom KPI reporting built on your existing data.">
<meta property="og:title" content="OpSight Manufacturing — Operational Intelligence for Manufacturers">
<meta property="og:description" content="Your production data, transformed into actionable intelligence. No new systems required.">
<meta property="og:url" content="https://opsightintel.com/manufacturing">
<meta property="og:type" content="website">
```

### OG Image

Create a simple 1200x630px image with your logo and tagline for social media previews. Save it as `og-image.png` in your repo root. This is what shows up when someone shares your link on LinkedIn or Twitter. Without it, shared links look empty and unprofessional.

---

## Priority 5: Submit to Google Search Console

- [ ] Go to https://search.google.com/search-console
- [ ] Click "Add property"
- [ ] Enter `https://opsightintel.com`
- [ ] Verify ownership — choose "DNS record" method:
  - Go to Cloudflare DNS settings
  - Add a TXT record with the value Google gives you
  - Click Verify in Google Search Console
- [ ] Once verified, go to "Sitemaps" in the left sidebar
- [ ] Enter `sitemap.xml` and click Submit
- [ ] Go to "URL Inspection" and enter `https://opsightintel.com/`
- [ ] Click "Request Indexing"
- [ ] Repeat URL Inspection for each page (intelligence, manufacturing)

Google will start crawling within a few days. Full indexing can take 1-4 weeks for a new domain.

---

## Priority 6: Submit to Other Search Engines

### Bing (also powers DuckDuckGo and Yahoo)
- [ ] Go to https://www.bing.com/webmasters
- [ ] Add your site, verify via DNS
- [ ] Submit your sitemap

### Naver (important for Korean market)
- [ ] Go to https://searchadvisor.naver.com
- [ ] Add your site and verify
- [ ] Submit your sitemap
- [ ] This is critical if you want Korean clients to find you

---

## Priority 7: Build Backlinks (How You Get Found)

A new domain with zero backlinks will rank near the bottom of search results even after indexing. You need other websites to link to yours.

### Quick wins (do this week):
- [ ] Post on LinkedIn announcing OpSight Intelligence — link to the site
- [ ] Add the URL to your LinkedIn profile (website field)
- [ ] Add the URL to your GitHub profile
- [ ] If you have a Twitter/X account, post about it and pin the tweet
- [ ] Create a GitHub organization for OpSight — the org profile can link to your site

### Medium-term (do within a month):
- [ ] Write a blog post on Medium or dev.to about AI agent guardrails — link to your site
- [ ] Write a blog post about fraud intelligence or manufacturing analytics
- [ ] Answer relevant questions on Stack Overflow or Reddit with helpful answers that naturally reference your site
- [ ] Submit the open-source guardrails repo to GitHub — the README links back to your site
- [ ] Reach out to the contacts from the Icon Megazone Cloud event

### Long-term (ongoing):
- [ ] Guest posts on security blogs
- [ ] Speak at meetups (Seoul tech community)
- [ ] Get listed in directories (Product Hunt, AlternativeTo, etc.)
- [ ] Case studies with early customers

---

## Priority 8: Analytics (Know Who's Visiting)

- [ ] Add Google Analytics or a privacy-friendly alternative (Plausible, Umami, or Cloudflare Web Analytics which is free and already in your Cloudflare dashboard)
- [ ] Cloudflare Web Analytics: Go to Cloudflare dashboard > Analytics & Logs > Web Analytics > enable it and add the JS snippet to your HTML
- [ ] This tells you how many people visit, which pages they view, and where they come from

---

## Summary — What to Do Today

| Step | Time | Impact |
|------|------|--------|
| Fix Cloudflare bot blocking | 5 min | Unlocks everything else |
| Add robots.txt | 2 min | Allows crawlers |
| Add sitemap.xml | 5 min | Tells crawlers what to index |
| Add meta tags to HTML | 15 min | Better search results and social previews |
| Submit to Google Search Console | 10 min | Starts the indexing process |
| Submit to Naver | 10 min | Korean market visibility |
| Post on LinkedIn | 10 min | First backlink and social signal |
| Enable Cloudflare Web Analytics | 5 min | Start tracking visitors |

**Total: about 1 hour of work. After that, your site goes from invisible to discoverable.**

---

## Expected Timeline After Fixes

| When | What happens |
|------|-------------|
| Day 1 | Cloudflare fixed, crawlers can access site |
| Day 2-3 | Google crawls your submitted URLs |
| Week 1-2 | Pages start appearing in Google results |
| Week 2-4 | Full indexing, search ranking improves with backlinks |
| Month 2+ | Organic traffic begins if you've been posting content and building links |
