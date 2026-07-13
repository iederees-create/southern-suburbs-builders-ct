# Public Demo Verification — Southern Suburbs Builders

**Deployment commit:** `b93dd73` (merge of `release/southern-suburbs-builders` into `main`)
**Deployment URL:** https://iederees-create.github.io/southern-suburbs-builders-ct/
**Deployment method:** GitHub Pages, source = `main` branch, root (`/`) — pre-existing
configuration on the repo, unchanged by this release.
**Verified:** live, publicly, over HTTPS — not from a local build.

## Pages checked (all HTTP 200 except the intentional 404 case)

| Path | Result |
|---|---|
| `/` (homepage) | 200, correct `<title>`, zero console errors |
| `/privacy.html` | 200 |
| `/terms.html` | 200 |
| `/disclaimer.html` | 200 |
| `/nonexistent-page.html` | 404, and the response body is the **custom** `404.html` ("Page Not Found \| Southern Suburbs Builders" / "Sorry, we couldn't find that page"), not GitHub's generic 404 |
| `/favicon.svg` | 200 |
| `/og-image.svg` | 200 |
| `/style.css` | 200 |
| `/app.js` | 200 |
| `/planner.js` | 200 |
| `/site-config.js` | 200 |
| `/sitemap.xml` | 200 |
| `/robots.txt` | 200 |

## Features checked live (real browser, real public URL, not localhost)

- **Homepage**: hero, trust bar, services grid with 6 jump-anchored cards,
  process steps, gallery placeholders, about/team, service areas, why-choose-us,
  stats, testimonials, FAQ, contact/hours, footer — all rendered from
  `site-config.js` with zero console errors.
- **Mobile navigation**: at a 390×844 viewport, the hamburger opens a
  full-height (780px) off-canvas panel; `document.documentElement.scrollWidth`
  equals `clientWidth` (no horizontal overflow). Screenshot captured.
- **Services**: all 6 service cards (Renovations/Extensions/New Builds/
  Paving/Boundary Walls/Project Management) present with working jump-chips
  and expandable detail.
- **Project gallery**: renders as clearly labelled placeholder cards
  ("Replace with a real project photo"), not fabricated photography.
- **Planner**: exercised live in-page via `window.RenovationPlanner` against
  the real `window.SITE_CONFIG` served from this exact URL — a boundary-wall
  scenario (15 linear metres, Premium finish, difficult site access) returned
  a correct budget range (R43,000–R96,500, Medium complexity), confirming the
  calculation engine and its config wiring both work correctly on the actual
  deployed asset, not just in local testing.
- **Quote form**: present, config-driven project-type options populated.
- **Privacy / Terms / Estimate Disclaimer pages**: load correctly, each
  carries its "starting-point template, not legal advice" callout.
- **404 behaviour**: confirmed above — custom page, not GitHub's default.
- **Metadata**: `<link rel="canonical">` and `<meta property="og:url">` both
  correctly read `https://iederees-create.github.io/southern-suburbs-builders-ct/`
  (the bug found and fixed in Phase 4 is confirmed live, not just locally).
- **Favicon / Open Graph image**: both fetch with HTTP 200 from their real
  public paths.
- **Sitemap / robots.txt**: both live and pointing at the correct domain.
- **Asset loading**: `style.css`, `app.js`, `planner.js`, `site-config.js`
  all load with HTTP 200 and no console errors on the live page.

## Unresolved deployment warnings

None. No console errors, no broken asset paths, no 404s on expected
resources, no mismatched metadata.

## Note on scope

This verification covers the deployed **website only**. Etsy listing images/
video (Phase 6), the buyer package (Phase 7), the Complete Product Pack
(Phase 10), the portfolio update (Phase 11–13), and the Etsy draft itself
(Phase 17–18) are separate, later phases of this release and are not implied
by this document.
