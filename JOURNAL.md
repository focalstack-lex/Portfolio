# Development Journal — Portfolio Lex

## [2026-10-11] Severus Design Pass (portfolio, landing, gallery, 404)

### Summary
- Typography: Geist replaces Inter as the voice face on portfolio, index, gallery, 404 and the chatbot; JetBrains Mono stays for data. Follows Typography Anti-Slop (Inter headlines at 700 are the generated-page tell).
- Grey ladder: muted `#999999` to warm `#a1a19e`, new `--text-faint: #787875` for years, category tags and case study labels, so reading order runs name > detail > metadata.
- Removed the "FOCAL STACK // CODE x CREATE" eyebrow pill above the Create heading (Anti-Eyebrow-Pill Directive) and its CSS.
- Case study de-boxed: problem/solution, features and facts use one hairline plus space instead of three rows of filled cards. Unverifiable metrics ("100% Fund Visibility", "0 Unverified Edits") replaced with facts from docs/portfolio-content.md (domain, sign-in restriction, 1.0-5.0 scale, CSV import).
- Photo grid: 3 columns at 1024px and up, 300px rows, upper-third crop bias; 8 photos now 1248px tall instead of 3626px. Filtered views drop spans so rows close without holes. Removed the heavy hover shadow.
- Gallery hand-off: removed the duplicate top "EXPLORE ALL SHOOTS" button; end-of-grid banner is now a hairline row with an underlined link instead of a filled box and white button.
- Non-clickable stack and gear rows lost `tabindex="0"` and their hover shift (11 rows).
- Footer headline: "LET'S BUILD SOMETHING REAL."
- docs/design-system-prompt.md updated to the new font and grey rules.

### Verification
- Browser preview at 1280px and 375px: `document.fonts` reports Geist 400-700 and JetBrains Mono loaded; no horizontal overflow on portfolio or landing at 375px.
- Grid geometry measured: all view 4 rows no holes; wedding, portraits and christening filters each one uniform row.
- Contrast: muted 7.87:1, faint 4.60:1 on `#050505`.
- `node --check portfolio.js` passed. Console errors limited to `/api/github-contributions` 404 (Vercel-only function).

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

## [2026-10-14] Tote product page at /tote

### Summary
- Added `tote/` as an extension page of the portfolio (www.codewithlex.site/tote) instead of a new domain. Built from the "Tote Website" Figma file (Desktop 1440 and Mobile 375 frames): nav, hero with a Find screen mock, feature band, Clean up and privacy section, install card with three steps, footer. Plain HTML and CSS, no JavaScript.
- Assets live under `tote/assets/`: the official Tote logo (`tote-logo.svg`, master in the Tote repo `brand/`), app icon favicons, 19 interface icons exported from the design, and Atkinson Hyperlegible Next (400 to 800) self-hosted with its SIL OFL license (`fonts/OFL.txt`).
- The installer is served from `tote/download/Tote_0.1.0_x64-setup.exe` (4,266,036 bytes). Because it is unsigned, the page shows its SHA-256 (8d5c3812c8f19c2fbfe373a565fe7b4757f73722df98ddbd6344c510ca57b852) under the download button, and the steps explain the SmartScreen prompt.
- `vercel.json`: rewrite `/tote` to `/tote/index.html` (the site has no clean URLs), a strict Content-Security-Policy on `/tote` paths only (`script-src 'none'`, self-hosted styles, images and fonts), a one-week cache on `/tote/assets`, and `Content-Disposition: attachment` with `application/octet-stream` on `/tote/download`. Every page asset uses an absolute `/tote/...` path so `/tote` works with or without a trailing slash.
- `sitemap.xml` gains the `/tote` URL (same host as the existing entries); README lists the page and how to ship a new Tote version.

### Verification
- Playwright on a local `serve` of the repo at 1440, 1280, 1024, 768, 375 and 320 px: no horizontal overflow, no broken images, no console errors or failed requests, every link and button at least 40 px, Atkinson Hyperlegible Next loaded (h1 56px at desktop, 40px on phones). Screenshots compared with the Figma frames.
- Every SVG under `tote/assets` parses as XML; installer SHA-256 matches the Tote release build; secret scan, dash and emoji check clean; `vercel.json` parses.

## [2026-10-14] Tote page: shorter mobile scroll

### Summary
- Lex reported long scrolls on phones (stacked tall feature and step cards). Below 900px the three features and the three install steps are now compact rows (badge or number beside the text, 16px padding, 19px and 17px titles); phone section spacing is tighter (band, Clean up, install card); the SHA-256 line is folded into a "Check the file (SHA-256)" disclosure (native details element, 44px tap target, no JavaScript).

### Verification
- Playwright at 1440, 1280, 1024, 768, 375 and 320px: no overflow, no broken images, no console errors or failed requests, no tap target under 40px. Page height at 375px went from 4305px to 3626px, at 768px from 3894px to 3431px; mobile screenshots reviewed.
