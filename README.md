# silasdray.com

The author site for Silas Dray, the pen name behind the *Ninety-Four* serialized novel and its sequels.

Built with Jekyll, served by GitHub Pages.

## Status

Phase A — pre-podcast landing page. Single page, single CTA (email signup placeholder). The marketing site grows when the podcast launches:

- **Phase A (now):** "Notify me at launch" landing page. Done.
- **Phase B (~2 weeks before podcast Ep 1):** Series landing page with embedded podcast player (Transistor); per-episode landing pages.
- **Phase C (~6 weeks before book release on KDP):** Buy links for ebook + paperback + audiobook (Findaway-wide); press / ARC distribution page.

Phases B and C are documented in the dystopian-series project's `business/website-and-podcast-automation.md`.

## Local development

```bash
bundle install              # first time only
bundle exec jekyll serve    # http://localhost:4000
```

## Deployment

Pushes to `main` auto-deploy via GitHub Pages. Custom domain (`silasdray.com`) is configured via the `CNAME` file in this repo plus DNS A/AAAA records at the registrar pointing to GitHub Pages's apex IPs.

## Architecture

- `_config.yml` — Jekyll site config
- `_layouts/default.html` — single layout used by all pages
- `assets/css/style.css` — all styling (literary-dark, restrained, no JS)
- `index.md` — landing page content
- `CNAME` — custom domain marker for GitHub Pages

No JavaScript. No tracking pixels. No fonts loaded from Google. The page is static text plus a stylesheet — total payload under 5 KB on first paint.

## Why no email service yet

The signup is a `mailto:` link rather than a ConvertKit/Buttondown form because the email platform decision is still open in `business/publishing-and-revenue.md`. When that locks, swap the link for the chosen service's form embed.

## Pen-name discipline

This is Silas Dray's site. Real-name attribution does NOT appear here. No author photo. No "the author lives in..." bio. Silas Dray is a ghost identity by design; the site preserves that boundary.
