# Final Website QA — Southern Suburbs Builders

Commit tested: `25474c3` (release/southern-suburbs-builders)

## Baseline issues from `handoff/codex/BASELINE-AUDIT.md` — status

Codex's baseline audit inspected the **old, pre-rebuild** site
(`clients/southern-suburbs-builders/index.html` in the `ct-lead-gen`
monorepo — placeholder branding "Apex Structural (Node--40)", a WhatsApp
link referencing "Civic Core Construction", external Google-hosted
agent-chat scripts, mojibake/BOM in the CSS, and unsupported claims
"4.9 Stars" / "Fully Insured" / "24hr Response Time" / "200+ Jobs
Completed" / "100% Satisfaction Rate"). All of these are confirmed **fixed**
in the merged repo — none of that content exists anywhere in the current
`index.html`/`style.css`/`site-config.js` (verified by grep; see
`handoff/FINAL-PRODUCT-FACTS.json` → `unsupported_claims_removed_from_original_site`).

## Commands run and results

```
$ npm test
tests 25
pass  25
fail  0
```
Covers area calculation, budget ranges, finish multipliers, invalid/zero/
negative input handling, summary generation, WhatsApp/email encoding,
reset, disabled-budget mode. No NaN/Infinity/negative output possible —
asserted directly in the suite.

```
$ node -c app.js && node -c planner.js && node -c site-config.js
app.js OK
planner.js OK
site-config.js OK
```

```
$ npx htmlhint index.html privacy.html terms.html disclaimer.html 404.html
Scanned 5 files, no errors found.
```

```
$ node scripts/release/scan-secrets.js .
Secret scan passed: /home/iedrees/Workspace/release-build/southern-suburbs-builders-ct
```

```
$ node tests/release/test-release-validators.js
scan-secrets passed
validate-media passed
validate-product-pack passed
validate-zip-content passed
```
(`validate-media.js` and `validate-product-pack.js` require a built product-pack
directory to run meaningfully against real content — that happens in Phase 10;
this run confirms the validator tooling itself is sound.)

## Live browser re-verification (chrome-devtools MCP, local static server)

- Page load: zero console errors/warnings.
- Corrected metadata confirmed live: `canonical` and `og:url` now both read
  `https://iederees-create.github.io/southern-suburbs-builders-ct/` (fixed a
  real bug found during this review — see below).
- **Lighthouse (desktop, navigation mode)**: Accessibility 100, Best
  Practices 100, SEO 100, Agentic Browsing 100. 56/57 audits passed;
  Cumulative Layout Shift 0.99/1 (displayValue 0.042, well within the
  "good" <0.1 threshold) — unchanged from the pre-merge build session,
  confirming the merge did not regress anything.
- **Planner edge case, live**: ran `RenovationPlanner.runPlanner()` in-page
  with `totalFloorArea: "-50"`, `lengthM: "0"`, `widthM: "-3"` — result:
  `quantity: null`, `budget.computable: false` with a human-readable reason,
  and the generated summary text contains no `NaN`/`Infinity` substring.
  Matches the unit-test coverage for invalid/zero/negative input.
- **Mobile viewport (390×844)**: hamburger menu opens to full viewport
  height (533px measured, `top: 64px`), `document.documentElement.scrollWidth`
  equals `clientWidth` (no horizontal overflow). Both are regressions that
  were found and fixed during the original build session (backdrop-filter
  containing-block bug, off-canvas-menu overflow bug) — reconfirmed intact
  after the merge.

## Bug found and fixed during this QA pass

**Wrong canonical/OG/sitemap domain.** The original build session (working
inside the `ct-lead-gen` monorepo, before this release task specified the
real repository name) guessed the public demo would live at
`.../southern-suburbs-builders-template/`. This release task confirmed the
actual repository is `iederees-create/southern-suburbs-builders-ct`. Fixed
in `index.html` (canonical link, `og:url` meta, and the `GeneralContractor`
JSON-LD `url` field), `sitemap.xml`, and `robots.txt` — all now point to
`https://iederees-create.github.io/southern-suburbs-builders-ct/`.

## Full edge-case matrix (planner) — carried forward from the build session, reconfirmed unaffected by the merge

| Case | Result |
|---|---|
| Every project type (9) | Each resolves to its configured rate band, unit (sqm vs. linear-metre for boundary walls), and default trade checklist |
| Every finish level (Essential/Standard/Premium/Custom) | Budget scales correctly; Custom triggers an explicit consultation-required assumption |
| Dimensions (length × width) | Computes area correctly; rejects non-numeric/zero/negative |
| Total area override | Takes precedence over dimensions when both provided |
| Multiple rooms/storeys | Storey count feeds the complexity multiplier and indicator |
| Invalid input (text in numeric field) | Rejected by `parsePositiveNumber`, treated as absent, surfaced in "Missing Information" |
| Blank input | Project type is the only hard requirement; everything else degrades gracefully |
| Zero / negative input | Never accepted as a valid quantity; never produces a zero/negative budget figure |
| Decimal input | Accepted and preserved (`round2`) |
| Very large input | Sweep-tested at `99999999` — still finite, non-negative, rounded correctly |
| Budget enabled / disabled | Both modes unit-tested and live-verified; disabled mode shows no numeric figures |
| Currency configuration | Reads `planner.currency` from config; formatter is currency-agnostic |
| Finish multipliers | Essential < Standard < Premium, asserted directly |
| Trade selection | Adds configured percentage to the range; merges with project-type defaults, de-duplicated |
| Summary generation | Plain-text, never contains `NaN`/`Infinity`/`undefined` |
| Missing-information logic | Flags every unfilled recommended field, clears once filled |
| Photo checklist | Varies by project type, falls back to a generic list |
| Copy / Print / Download summary | Clipboard API with textarea-select fallback; print isolates the summary via a body class + `@media print`; download creates a client-side `.txt` Blob |
| WhatsApp / email encoding | URL-encoded via `encodeURIComponent`; unit-tested against special characters (`&`, spaces, newlines) |
| Reset | Returns a fresh, independent default-input object each call |
| Keyboard-only operation | Skip link, `:focus-visible` ring, keyboard-operable FAQ/service accordions, Escape closes mobile nav and the confirm modal |
| Mobile operation | Verified at 390px viewport, see above |
| No message sent without confirmation | WhatsApp/Email/Site-Visit actions all route through an explicit confirm modal; `window.open` verified (via a patched stub) to fire only after "Confirm & Send" is clicked, never on the initial action click |

## Outcome

**Website QA: PASS.** No known open defects. All validator tooling
provided by `agent/codex-release` runs clean against the current repo
state. Ready for Phase 5 deployment.
