# Development Journal — Portfolio Lex

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
