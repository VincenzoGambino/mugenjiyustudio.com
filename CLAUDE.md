# CLAUDE.md — Italy Company Website (adapted from UK site)

## Context
Two companies, same owner, same services, different countries and domains:
- **UK company**: existing site, bilingual (English + Italian)
- **Italy company**: new site, to be based on the UK site's structure/design, Italian only

Goal: reuse the UK site's layout, design system, and Italian copy as a *starting point*, not a direct copy — to avoid duplicate-content SEO issues across the two domains.

## What can be reused as-is
- Page layout, templates, code, design system
- Overall site structure (same page types: home, services, about, contact)
- Bio/personal background content (inherently identical — same person)

## What must change
- **Branding**: logo, colors, contact details, company name/legal entity per domain
- **Copy**: do NOT copy the Italian pages from the UK site verbatim onto the Italy domain. Rewrite/adapt them — moderate rewriting is enough (restructure sentences, swap examples/case studies to reference Italian clients/market, adjust CTAs and tone for local audience).
- **Language**: Italy site should be **Italian only** — drop the English version unless there's a specific reason to target English-speaking clients from Italy.

## SEO setup checklist
- [ ] Separate Google Search Console property for each domain
- [ ] Self-referencing canonical tags on each domain (never cross-domain canonicals)
- [ ] Unique meta titles/descriptions per domain, not duplicated from the UK site
- [ ] If content overlap remains between languages/domains, consider `hreflang` tags to signal alternate-language relationship (only relevant if cross-linking the two sites)
- [ ] Distinct testimonials/case studies per site where possible, to reflect local market credibility

## Priority when rewriting pages
1. Service pages — highest duplicate-content risk, rewrite most heavily
2. Homepage — rewrite messaging/CTAs for local market framing
3. About/bio — can stay close to original (same person, same story)
4. Contact — just swap details, no SEO concern here

## Domains
- UK site (source, being cloned from): **stripedcodex.com**
- Italy site (this repo, target): **mugenjiyustudio.com**

## Technical cleanup (static site, cloned repo)
Since this repo started as a clone of stripedcodex.com, search the whole codebase for any hardcoded reference to the old domain and update it — copy changes alone are not enough. Check specifically:

- [ ] `sitemap.xml` — all URLs still point to stripedcodex.com, must be regenerated for mugenjiyustudio.com
- [ ] `robots.txt` — sitemap reference and any absolute URLs
- [ ] Canonical link tags (`<link rel="canonical" ...>`) in every page's `<head>` — must self-reference mugenjiyustudio.com, not stripedcodex.com
- [ ] `hreflang` tags, if present, pointing to stripedcodex.com pages
- [ ] Open Graph / Twitter meta tags (`og:url`, `og:image` absolute paths, etc.)
- [ ] Analytics / tracking IDs (Google Analytics, Search Console verification tags, Facebook Pixel, etc.) — these should be separate per domain, not shared
- [ ] Any hardcoded absolute URLs in JSON-LD structured data (Organization schema, LocalBusiness schema, etc.) — legal entity name, address, and domain must match the Italy company
- [ ] Internal links using absolute URLs (e.g. `https://stripedcodex.com/services`) instead of relative paths
- [ ] Favicon, manifest.json, and any PWA-related absolute URLs
- [ ] Email addresses and forms endpoints (if using a static form service like Formspree, these are often tied to a specific domain/account)

A simple first pass: `grep -ri "stripedcodex" .` across the repo to catch anything missed above.
