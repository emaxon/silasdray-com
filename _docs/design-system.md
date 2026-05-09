# silasdray.com — Design System

> **The contract.** Everything visual on silasdray.com obeys this document. Changes argue against the spec; the spec changes are versioned in the CHANGELOG at the bottom.
>
> Locked: 2026-05-08 by the site-strategy roundtable in [the dystopian-series session note](https://github.com/emaxon/dystopian-series/blob/main/docs/session-notes/2026-05-08-silasdray-com-site-strategy.md).

## What this design system serves

silasdray.com is the public-facing site for the pen name behind the *Ninety-Four* serialized novel and its sequels. The design must:

- Match the worlds Silas Dray writes — invisible-dystopia present-day America; literary-clinical; pen-name-anonymous
- Read as a **document**, not as an application — no dashboards, cards, dropdowns, or chrome that suggests software
- Survive a 30-week serialized podcast season and a planned trilogy without aesthetic drift
- Honor the pen-name discipline: no author photo, no biographical details, no assumption of personality beyond the work

It must NOT look like:

- An EPM Labs content/affiliate site (LushLawns, HarvestHomeGuides, etc.) — those are bright, friendly, conversion-funnel-coded. Wrong audience.
- A SaaS marketing page — flashy, animated, hero-image-heavy. Wrong register.
- A typical author landing page — author photo, "Buy My Book Now" CTA, social-proof testimonial wall. Pen-name discipline forbids most of that.

## 1. Typography

Two faces. Self-hosted, Latin subset, woff2.

| Role | Family | Weight(s) | Notes |
|---|---|---|---|
| Body / long-form prose | IBM Plex Serif | 400 (regular), 400 italic, 600 (semibold) | 18px / 1.7. Reading column 65ch. No first-line indent (this is web, not print). |
| Display / chrome / metadata | IBM Plex Mono | 500 (medium) | All headings, wordmark, nav, footer, dates, form labels, button labels. `font-feature-settings: 'tnum' 1` set globally so Mara's "numbers as shapes" perceptual frame renders as type. |

**Why this stack:** Plex Serif's institutional/clerical edge matches a federal-data-analyst protagonist. Plex Mono's tabular numerals render the number-shape passages correctly. Mono numerals are voice, not decoration.

**Font files** (in `/assets/fonts/`, all woff2, all under 16KB each after Latin subsetting):

- `IBMPlexSerif-Regular.woff2` (15KB)
- `IBMPlexSerif-Italic.woff2` (16KB)
- `IBMPlexSerif-SemiBold.woff2` (15KB)
- `IBMPlexMono-Medium.woff2` (10KB)

Total font payload: 56KB.

**Loading:** `font-display: swap`. Two preload links in `_includes/head.html` (Regular serif + Medium mono — the LCP-critical pair). No woff fallback; modern-browser only.

## 2. Palette

Six tokens. Single accent. **Dark inversion** (locked 2026-05-09 by Evan; original light palette retired — see CHANGELOG).

| Token | Hex | Role | Contrast on `--paper` |
|---|---|---|---|
| `--paper` | `#14110F` | Page background. Deep warm near-black. | — |
| `--ink` | `#EDE6D9` | Body text, all primary type. Warm cream. | 15.2:1 (AAA) |
| `--ink-muted` | `#A39C8E` | Secondary text, captions, metadata, fine print. | 6.9:1 (AA, near-AAA) |
| `--rule` | `#3D362F` | Hairline borders, dividers, form outlines. | 1.6:1 (decorative only — never used as text) |
| `--mark` | `#D9614F` | Single accent: links, primary CTAs, focus rings, wordmark. Rust. | 5.2:1 (AA) |
| `--mark-soft` | `#E8867A` | Hover/active state for `--mark`. | 7.3:1 (AAA) |

**Rule:** if something is interactive or important, it is rust. Otherwise it is ink or muted ink. There is no second accent color, ever.

**Why dark instead of light:** the warm-paper-document framing the original synthesis chose was tonally adjacent to literary fiction generally but did not match the **invisible-dystopia** register of the books specifically. Dark serves the dystopian theme directly. Same restraint, same mono-numerals, same single-accent discipline — just inverted. The rust accent (`--mark`) replaces the original oxblood because oxblood at the original `#6B1F1A` fails WCAG AA on near-black (~1.5:1); rust holds AA at 5.2:1 with the same warm-red family character.

**Auto dark on light-mode systems:** the site does not respect `prefers-color-scheme: light`. The site is dark for everyone. This is deliberate per the dystopian framing.

## 3. Spacing scale

8px vertical rhythm. Powers-of-two-leaning multiples:

`4 · 8 · 12 · 16 · 24 · 32 · 48 · 64 · 96 · 128` px

Mapped to CSS custom properties as `--s-1` through `--s-32` (number is the rem-equivalent × 4 floor).

**Section gaps:** 64–96px (`--s-16` to `--s-24`)
**In-section gaps:** 16–24px (`--s-4` to `--s-6`)
**Reading column max:** 720px (`--col-read: 65ch` ≈ 720px at 18px/1.7)
**Page wrap max:** 1040px (`--col-page` — chrome-only)
**Form column max:** 480px (`--col-form`)

## 4. The "94" rule

The numeral `94` has reveal-value within the book and **does not appear in site chrome.**

- No logomark uses it
- No favicon glyph
- No watermark, ornament, or palette-swatch label
- Page wordmark spells out **NINETY-FOUR**
- The numeral appears only inside the prose where Mara writes it down (Ch 1 "ninety-four sits in the middle of the decade" passage)

If a future feature wants to use `94` decoratively, the web-designer must sign off and the rationale must beat "we don't normalize it."

## 5. Components

### 5.1 Wordmark (header)

`SILAS DRAY`, oxblood, mono medium, letter-spacing 0.12em. Links to `/`. No logomark, no favicon glyph based on the wordmark.

### 5.2 Site nav (header)

Inline horizontal list, mono medium, ink color (rust for SUBSCRIBE only). 24px gap between items, smaller on mobile. No icons. No dropdowns.

**Phase A links:** `NINETY-FOUR · ABOUT · SUBSCRIBE`. NOTES is hidden until the first note ships (the page exists at `/notes/` for direct linking but is not surfaced in nav while empty — empty rooms in primary nav read as abandoned, not restrained). Restore `NOTES` link via header.html when content lands. See silasdray-com#21.

### 5.3 Site footer

Two-line. First line: italic serif distribution sentence in ink color (with rust em). Second line: mono single-line wordmark + copyright + legal links. Stacked vertically on mobile.

```
Find Ninety-Four on Apple Podcasts, Spotify, and YouTube Music when episode one drops.

SILAS DRAY     © 2026 · Privacy · Terms · Cookies · Disclosure
```

Footer wordmark is rust (same as header). Copyright + legal links are ink-muted. The distribution line is italic serif (matches body register, not chrome register) — a writer note, not metadata. No social icons, no email, no "built with" credit.

**Phase B trigger:** when episode one releases, the distribution-line copy changes from "when episode one drops" to platform-specific links. The line itself stays.

### 5.4 Subscribe form

Locked component. One label ("NOTIFY ME WHEN EPISODE ONE RELEASES"), one email input, one button ("SUBSCRIBE"), one fine-print line ("One email when the first episode releases. No other use."). Honeypot field invisible (`tabindex="-1"`).

Embedded on `/`, `/ninety-four/`, `/about/`, `/thanks/` (non-form summary). NOT on `/notes/` (deliberate; quiet placeholder), NOT on legal pages, NOT on `/404.html`.

### 5.5 Buttons

One button style: oxblood-on-paper rectangle, mono medium, no border-radius, no shadow. Hover lightens to `--mark-soft`. Focus ring is 2px ink outline.

There is no "secondary" button style. Phase A doesn't need one.

### 5.6 Body prose

Plex Serif Regular, 18px, 1.7 line-height, 65ch column max. Italic for emphasis. Bold (semibold weight 600) used sparingly for in-paragraph emphasis only — never for headings (those are mono).

### 5.7 Blockquote

2px ink-rule left border, 24px left padding, 18px italic-default body. Cite line below in italic, ink-muted, smaller (16px).

### 5.8 Three-paths list (landing only)

Below-the-fold on `/`. Three items: `THE NOVEL`, `NOTES`, `ABOUT`. Each: mono heading + italic serif lede + oxblood arrow link. Vertically stacked, 48px gap between items, top border separates from above-the-fold.

## 6. What we are NOT building

| Forbidden | Reason |
|---|---|
| Cards, badges, tags, chips | UI-product vocabulary; this is a document |
| Icons / icon set | None earn their cost at this scale |
| Carousel | Content fits; no carousel ever |
| Modal / dialog | Subscribe is inline; nothing else needs a modal |
| Tooltip | If something needs explanation, it's plainly written |
| Breadcrumbs | 4-page IA; the URL is the breadcrumb |
| Hover-reveal text or accordions | Either say it or don't |
| Motion beyond 100ms color transitions | No fades, slides, parallax, or scroll-triggered animation |
| Author photo, hero image, book cover | Phase A — pen-name discipline + no asset to ship yet |
| Dark mode | Locked: dark mode reads as application |
| Google Fonts | Self-host; no external font load |
| Tracking pixels beyond GA4 | One analytics provider, named in `/cookies/` |
| Social-proof testimonials | No audience yet, and pen-name discipline forbids most |

If a future feature wants something on this list, the web-designer signs off before the engineer builds. Not the other way around.

## 7. Accessibility floor

WCAG 2.2 AA is the floor, not the ceiling.

- All text/background pairs verified in section 2 (palette table)
- Focus indicators: `:focus-visible` outline 2px solid `--mark`, 3px offset
- Keyboard navigation: every interactive element reachable via Tab; logical focus order; no traps
- Semantic HTML: `<main>`, `<nav>`, `<header>`, `<footer>`, `<article>` used appropriately
- Single `<h1>` per page
- Alt text discipline: empty `alt=""` for decorative images (Phase A has no images at all)
- `prefers-reduced-motion: reduce` respected (motion globally disabled)
- `prefers-color-scheme: dark` deliberately NOT supported (out-of-scope by design)
- Form inputs have associated labels via `for=`/`id=`; required fields use the `required` attribute; error states use the browser's native validation UI
- The honeypot field has `tabindex="-1"` so keyboard users skip it

## 8. Performance budget

| Metric | Target | Rationale |
|---|---|---|
| First Contentful Paint | < 1.0s on 4G | Paper background + ink text; no blocking JS |
| Largest Contentful Paint | < 1.5s on 4G | LCP element is body text; preloaded fonts ship in same first round-trip |
| Cumulative Layout Shift | < 0.05 | Self-hosted fonts with `font-display: swap` accepted to slightly increase CLS in exchange for FCP win; layout-stable form input |
| Total CSS | < 10KB minified | Hand-rolled stylesheet; no framework |
| Total page weight (excl. fonts) | < 30KB | Markdown → HTML, single CSS file, no JS beyond GA4 |
| Total page weight (incl. fonts) | < 90KB | 56KB of woff2 fonts |
| JS budget | 0KB own + GA4 only | No interactive components in Phase A |

## 9. Implementation notes

- **Build:** Jekyll on GitHub Pages. Plugins: `jekyll-feed`, `jekyll-seo-tag`, `jekyll-sitemap`. No JS bundler, no transpiler, no Sass — straight CSS.
- **CSS approach:** Single `assets/css/main.css`. Custom properties at the top. No utility-class framework. **No Tailwind, no Bulma.** If a future maintainer wants Tailwind, revisit then; for Phase A, hand-rolled.
- **Asset paths:** Fonts at `/assets/fonts/`, CSS at `/assets/css/main.css`. No image assets in Phase A.
- **Source of truth for tokens:** This file. CSS custom properties in `main.css` mirror the values here. If they drift, this file wins; update CSS to match.
- **Source comment in CSS:** The CSS file has a header pointing back here so future-me editing the CSS knows where the canonical spec lives.

## 10. Future-change protocol

1. If a change is proposed (new component, new color, new typography, etc.), the web-designer must sign off before it lands.
2. Append an entry to the CHANGELOG below.
3. Update both this doc AND `assets/css/main.css` in the same commit.
4. If the change affects the playbook, propose updates to `~/Sites/agency/docs/playbooks/` in the same change.

## CHANGELOG

### 2026-05-09 — three principal-overrides after first review

Evan reviewed the deployed Phase A site and overrode three locked decisions. All three preserve the underlying restraint principles; they revise specific lock outcomes.

**Override 1: dark inversion replaces warm-paper.** The original synthesis locked `--paper` as `#F4F1EA` (warm off-white) on the showrunner's reasoning that "dark mode reads as application; this site reads as document." Evan's read on the deployed site: warm-paper served the literary register but did not serve the **invisible-dystopia** register of the books specifically. Dark inversion lands the dystopian framing directly. Implementation: full palette flip with the accent rebalanced from oxblood `#6B1F1A` (fails WCAG AA on near-black, ~1.5:1) to rust `#D9614F` (5.2:1, AA). Same family, brighter. Original light palette retired — not preserved as a toggle. The site is dark for everyone.

**Override 2: footer carries a distribution sentence.** Original synthesis explicitly rejected pre-launch distribution language as "brand-corrosive — date-fake is brand-corrosive." Evan's read: pre-launch traffic is low enough that the negative impact is minimal, and the footer answers a natural question ("where will I find this?"). Restored line: *"Find Ninety-Four on Apple Podcasts, Spotify, and YouTube Music when episode one drops."* Italic serif, ink color with rust em on the title. Phase B updates the wording to platform-link form when episode one ships.

**Override 3: /notes/ hidden from nav until content lands.** Original synthesis locked the `NO ENTRIES` empty state on the site-editor's argument that "silence is stronger than wink." Evan's read: an empty page surfaced in primary nav reads as abandoned regardless of empty-state copy. The page still exists at `/notes/` and is still indexed; the navigation link is removed until the first note ships. Tracked in silasdray-com#21.

### 2026-05-08 — initial lock

Tokens, components, accessibility floor, performance budget, and "what we are not building" all locked from the site-strategy roundtable synthesis. Implementation plan: 17 GitHub issues across Sprint 1 (rebuild), Sprint 2 (analytics + search), and Sprint 3 (content swap). See `https://github.com/emaxon/silasdray-com/issues`.
