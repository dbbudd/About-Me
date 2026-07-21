---
version: alpha
name: Daniel Budd — Modern Academic Industrial
description: Visual identity for danielbudd.com.au and the Barriers app site. Navy authority, gold accent, minimalist geometry, no-waffle restraint.
colors:
  navy: "#1F457F"
  navyDeep: "#0E2A50"
  gold: "#FFD84D"
  goldDeep: "#E8A020"
  ink: "{colors.navyDeep}"
  bodyText: "#33435A"
  muted: "#5B6B82"
  paper: "#FFFFFF"
  canvas: "#F6F8FB"
  line: "#E3E9F2"
  heroText: "#CDDCF0"
typography:
  body:
    fontFamily: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.6
  h1:
    fontFamily: "{typography.body.fontFamily}"
    fontSize: 52px
    fontWeight: 800
    letterSpacing: -1px
  h2:
    fontFamily: "{typography.body.fontFamily}"
    fontSize: 26px
    fontWeight: 800
    letterSpacing: -0.3px
  kicker:
    fontSize: 13px
    fontWeight: 700
    letterSpacing: 6px
  eyebrow:
    fontSize: 11px
    fontWeight: 700
    letterSpacing: 2px
  tagline:
    fontSize: 20px
    fontWeight: 400
  caption:
    fontSize: 13px
    fontWeight: 600
rounded:
  bar: 3px
  button: 10px
  media: 12px
  card: 16px
  pill: 999px
  circle: 50%
spacing:
  contentMaxWidth: 880px
  pagePadding: 24px
  cardPadding: 32px
  sectionGap: 24px
  gridGap: 24px
  mediaGap: 20px
  galleryGap: 16px
  denseGap: 12px
components:
  card:
    backgroundColor: "{colors.paper}"
    rounded: "{rounded.card}"
    padding: "{spacing.cardPadding}"
  buttonPrimary:
    backgroundColor: "{colors.gold}"
    textColor: "{colors.navyDeep}"
    rounded: "{rounded.button}"
    padding: 12px 22px
  socialIcon:
    backgroundColor: "{colors.paper}"
    rounded: "{rounded.media}"
    size: 44px
  videoEmbed:
    backgroundColor: "#000000"
    rounded: "{rounded.media}"
  heroNavPill:
    textColor: "#FFFFFF"
    rounded: "{rounded.pill}"
    padding: 8px 14px
---

## Overview

The brand is **Modern Academic Industrial**: the authority of a university lecture theatre with the precision of an engineering drawing. It serves an Apple Distinguished Educator's personal site and the marketing page for the Barriers iPad app, and it must read as credible to three audiences at once — educators, conference organisers, and App Store reviewers.

The governing editorial principle is **no-waffle**: high signal, low noise. The visual system enforces the same discipline — few colors, one typeface stack, generous whitespace, and nothing decorative that doesn't carry meaning. When in doubt, remove.

## Colors

Navy is the voice; gold is the emphasis. `navy` → `navyDeep` gradients (160deg) form hero backgrounds and communicate institutional authority. Gold appears **only** as accent: the `h2` bar, primary buttons, hover borders, the kicker text, and the hero's circular gold motif. Gold is never a background for body content and never used for running text on white — its job is to direct the eye to one action or one heading per view.

Text hierarchy is three steps: `ink` for headings, `bodyText` for prose, `muted` for captions and secondary lines. On navy, use white for headings and `heroText` for supporting copy. `canvas` is the page background; content sits on `paper` cards separated by `line` borders. Hero images are always tinted with the navy gradient overlay (at ~0.88–0.92 opacity) so photography never competes with the palette.

All colors are defined as CSS custom properties in `:root` in `styles.css`. Reference the variables (`var(--navy)`, `var(--gold-deep)`, …) — never hardcode hex values in page markup.

## Typography

One system font stack everywhere — no webfonts, by design (performance and the Apple-native aesthetic). Hierarchy is achieved through weight and tracking, not typeface changes: display text is heavy (800) with tight negative tracking; labels (`kicker`, `eyebrow`) are small, bold, uppercase, with wide positive tracking in gold tones. Body text stays at 400/1.6 for comfortable reading. Nothing between 400 and 700 — the contrast between heavy and regular *is* the typographic style.

## Layout

A single centered column, `contentMaxWidth` (880px) with 24px side padding. Sections are either **cards** (`.card` — white, bordered, 16px radius, 32px padding) for prose content, or **full-bleed grids** (projects, videos, gallery) that sit directly on the canvas. Grids use CSS Grid with `auto-fit`/`auto-fill` and minmax columns so they collapse without media-query sprawl; the two fixed grids are `.support-grid` (1fr 1fr, text left / centered actions right, stacking under 820px) and `.shorts-grid` (6 → 3 → 2 columns at 820px/480px breakpoints). Vertical media uses 9:16 (`.shorts-embed`), horizontal uses 16:9 (`.video-embed`), screenshots use the iPad ratio 2778:1284.

## Elevation & Depth

Depth is used sparingly and almost never with shadows. Separation comes from borders (`line`) and background contrast (`paper` on `canvas`). The exceptions: the avatar (soft navy-tinted shadow), the lightbox image, and hover states — cards lift 2–3px on `translateY` with a `goldDeep` border. If a new element needs to feel interactive, prefer the hover-lift + gold-border pattern over adding shadows.

## Shapes

Geometry is rounded-rectangular and calm: 16px for containers, 12px for media and icon tiles, 10px for buttons, pills for floating navigation chips. The one expressive shape is the **gold circle** bleeding off the hero's top-right corner — it is the brand's signature mark; keep it on every hero. The `h2` gold bar (6×22px, 3px radius) is the section-level echo of the same idea.

## Components

- **Primary button (`.btn`)** — gold→goldDeep gradient (135deg), navyDeep text at 700, 12×22px padding. One primary action per section. There is no secondary button style; a plain navy text link is the secondary action.
- **Section heading (`h2` + `.bar`)** — every section title carries the gold bar. No exceptions; it's the scanning anchor.
- **Cards (`.card`, `.project-card`)** — white, `line` border, hover lift with gold border on interactive cards.
- **Social icons (`.social-icons`)** — 44px tiles, navy SVG glyphs, hover lift + gold border. Icons are monochrome minimalist — never brand-colored logos.
- **Video embeds** — always inside the rounded black frame, `loading="lazy"`. Vertical content in `.shorts-grid`, horizontal in `.video-grid`. A dormant `.video-card` click-through thumbnail pattern exists for when iframe weight matters.
- **Hero** — navy gradient (optionally over a tinted photo), kicker + h1 + tagline centered, gold circle motif top-right, pill nav chip top-left.

## Do's and Don'ts

**Do**

- Use `:root` CSS variables for every color; add new tokens there first, then here.
- Keep one gold-accented action per view; let whitespace do the layout work.
- Tint every hero photograph with the navy gradient overlay.
- Match new grids to the existing minmax/auto-fit pattern and existing breakpoints (820px, 480px).
- Preserve the email-obfuscation pattern (`data-u`/`data-d`) for any contact link.

**Don't**

- Don't introduce webfonts, new typefaces, or intermediate font weights.
- Don't use gold as a text color on white, or as a large background fill.
- Don't add drop shadows to cards or buttons; borders and lift-on-hover are the depth language.
- Don't use pure black — `navyDeep`/`ink` is the darkest value (media frames excepted).
- Don't add decorative imagery, badges, or animation that doesn't serve comprehension — no-waffle applies to pixels as much as prose.
