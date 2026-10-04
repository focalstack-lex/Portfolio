# Development Journal — Portfolio Lex

## [2026-10-04] Share, Search, Deploy and Accessibility Hardening

### Summary
- Open Graph and canonical tags on index, gallery and resume pages.
- `robots.txt` and `sitemap.xml` (5 public pages, `/api/` disallowed).
- `vercel.json`: nosniff, Referrer-Policy, SAMEORIGIN framing, Permissions-Policy, 7-day cache on `/assets/`.
- `.vercelignore`: docs, tooling and unused originals (bnw.jpg, colored.jpg, coelgu-demo.mov, about 22 MB) no longer deployed.
- Removed dead/mistyped `<source>` children from the showcase video (the `src` attribute already served the MP4).
- Photo lightbox moves focus to the close button on open and back to the tile on close.
- Branded `404.html`; README rewritten to match the current site and repo URL.

### Verification
- `python` XML parse of sitemap.xml and JSON parse of vercel.json passed; `node --check portfolio.js` passed.
- Checked that nothing at runtime fetches `docs/` or the excluded originals before ignoring them.

## [2026-09-28] Client Readability Pass (portfolio.html, portfolio.css)

### Summary
- Hero lede plus GET IN TOUCH / VIEW RESUME (Tech) and GET IN TOUCH / OPEN FULL GALLERY (Create) links, so name, school and contact path sit above the fold instead of in section 03/04.
- Section indices made sequential: Tech 01-04, Create 01-03 (previously skipped unnumbered sections).
- Replaced emoji-prone glyphs (play, grid, close) with inline SVG icons.
- Lightbox `data-caption` / `data-meta` aligned with the visible tile captions (they disagreed on titles and lens focal lengths).
- Open Graph + canonical tags for link previews on Messenger/Facebook.
- Mobile (<=580px): invisible 40px hit areas on links, 40px video HUD and carousel buttons, enlarged scrubber and dot hit zones, 9px floor on overlay labels (was 7.5px).
- Copy: removed trailing ellipsis on "Stories in stillness and motion".

### Verification
- Local preview (`npx serve`, port 5177) at 375px and 1280px: `scrollWidth == innerWidth` (no horizontal overflow), hero lede visible above the fold (top 312px at 375px), smallest text 9px, lightbox caption reads "Ring Shots · Intimate Ceremony · 55mm ƒ/1.8", screenshot toggle still switches panes, zero glyphs remaining.
- Console: only 404s are `/api/github-contributions` (Vercel function, unavailable locally, pre-existing).
- Diff scanned for em/en dashes: none added.

## [2026-09-19] Print Styles Optimization for Resume PDF

### Summary
- Updated `@page` CSS print rules in `resume.html` by setting `margin: 0`.
- Suppressed standard browser headers (date/time, document title) and footers (URL, page number count) during print and "Save to PDF" operations.
- Added explicit print padding (`padding: 0.6in 0.8in`) on the `body` container to maintain clean Harvard-format styling and content margins.

### Verification
- Verified CSS `@media print` rules in `resume.html`.

## [2026-09-19] Official System Name & Institutional Deployment Details

### Summary
- Updated system title to **College of Engineering Official Student Portal** across `resume.html`, `portfolio.html`, and `portfolio-code.html`.
- Added explicit deployment location details: **Cor Jesu College** (gated with `@g.cjc.edu.ph` institutional authentication).
- Updated project badges and descriptions in the resume and portfolio showcase cards.

### Verification
- Verified HTML markup in `resume.html`, `portfolio.html`, and `portfolio-code.html`.
