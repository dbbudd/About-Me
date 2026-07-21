# CLAUDE.md — danielbudd.com.au (About-Me site)

Personal website for Daniel Budd and the marketing/support site for the **Barriers: UDL Reflection** iPad app. Static HTML/CSS, no build step, no frameworks, no JS dependencies.

## 1. Strategic Purpose

This site serves four jobs, in priority order:

1. **App Store infrastructure for Barriers.** `barriers.html` is the app's official Marketing + Support URL and `barriers-privacy.html` is its Privacy Policy URL — both are on record in App Store Connect. Breaking these URLs (or renaming the files) breaks App Store compliance. Treat them as load-bearing.
2. **Professional landing page.** `index.html` establishes Daniel's authority as an Apple Distinguished Educator, speaker, author, and app developer — the destination for conference bios, LinkedIn, and speaking-engagement inquiries.
3. **YouTube funnel.** Video embeds (long-form on index, Shorts on barriers) bridge site visitors to the channel (https://www.youtube.com/@DanielBBudd) and back — part of the broader "Efficient Architect" strategy: YouTube → app launches → speaking → book.
4. **Proof of "Privacy by Design."** Barriers collects no data, has no accounts, and runs AI on-device. The site's copy leans on this differentiator; a future "Privacy by Design" video will slot into the reserved column of the Privacy Policy section on barriers.html.

Tone follows the "no-waffle" brand standard: direct, high-signal, minimal copy. Do not pad sections with marketing filler.

## 2. Technical Overview

- **Hosting:** GitHub Pages — repo `dbbudd/About-Me`, branch `main`, root. Custom domain via `CNAME` → `danielbudd.com.au` (HTTPS enforced). Deploy = commit + push to main; changes go live in ~1 minute.
- **DNS:** Crazy Domains. Nameservers must stay on `ns1/ns2.crazydomains.com` (a past outage was caused by lame delegation to `dnspackage.com`).
- **Stack:** Hand-written HTML + one shared stylesheet (`styles.css`). No build tooling, no JS frameworks — keep it that way.

### File map

| File | Role |
|---|---|
| `index.html` | Personal landing page: projects grid, bio, recent long-form videos |
| `barriers.html` | Barriers app: about + promo video, screenshot gallery, UDL rationale, support, privacy summary, related Shorts |
| `barriers-privacy.html` | Full privacy policy for the app (App Store Privacy Policy URL) |
| `privacy.html` | Site-wide privacy page |
| `styles.css` | Single shared stylesheet for all pages |
| `DESIGN.md` | Design-system spec (Google design.md protocol) — tokens + visual rules for agents |
| `CNAME` | Custom domain — do not delete or edit |
| `robots.txt`, `sitemap.xml` | SEO plumbing — update sitemap if pages are added |
| `images/` | All images, including favicons (`images/favicon-32.png`, `images/apple-touch-icon.png`) and per-project subfolders (`Barriers/`, `Geometry/`) |

### Conventions

- **Palette (Modern Academic Industrial, per project `design.md`):** navy `#1F457F` / deep navy `#0E2A50`, gold `#FFD84D` / deep gold `#E8A020` — all defined as CSS custom properties in `:root`. Use the variables, never hardcode.
- **Section pattern:** `<section class="card">` with `<h2><span class="bar"></span>Title</h2>` (gold bar accent). Full-bleed sections (project grid, video grids) omit `.card`.
- **Two-column card layout:** `.support-grid` — text left, action(s) right, centered; collapses to one column under 820px. Used by both Support and Privacy Policy sections on barriers.html (Privacy's right column is intentionally empty, reserved for the "Privacy by Design" video).
- **Video embeds:** 16:9 → `.video-embed` inside `.video-grid`; vertical Shorts → `.shorts-embed` inside `.shorts-grid` (6-across desktop, 3 tablet, 2 mobile). All iframes use `loading="lazy"`.
- **Email obfuscation:** support email is never plain text in source. Links use `class="email-link" href="#" data-u="dbbudd" data-d="gmail.com"`; inline JS assembles the `mailto:` at runtime. Preserve this pattern for any new contact links.
- **Screenshot gallery:** `.gallery` figures open in the shared lightbox (`#lightbox` + inline JS in barriers.html).
- **SEO/social:** every page carries canonical URL, OG + Twitter cards, and JSON-LD (`Person` on index, `SoftwareApplication` on barriers). Keep these in sync when copy changes.

### Gotchas (learned the hard way)

- YouTube embeds do **not** load from `file://` preview (null origin) — test over http(s), e.g. `python3 -m http.server`.
- Some crawlers/older iOS request `/apple-touch-icon.png` at the root by convention; icons now live in `images/`, so those requests 404 harmlessly.
- App preview videos for the App Store must be app-footage-only screen captures — marketing promos get rejected.
- JPG derivatives of screenshots are used on-page; matching PNG originals in `images/Barriers/` are source files, not referenced by HTML.

## 3. Current Status & Pending Work (as of 2026-07-21)

- **App status:** Barriers submitted to App Store review; manual release selected, to be aligned with YouTube Video 1 launch.
- **Pending on approval:** swap the App Store badge `href="#"` in the barriers.html hero for the real App Store link.
- **Reserved slot:** right column of the Privacy Policy section awaits the "Privacy by Design" video embed (`.video-embed` block).
- **Known asset issue:** the AI-generated lifestyle image (hands + iPad) has garbled text artifacts — needs a real screenshot composited before public use.
- **Possible optimization:** barriers.html carries 8 iframes; if load feels heavy, convert embeds to click-through thumbnail cards using the existing (currently unused) `.video-card` styles.
