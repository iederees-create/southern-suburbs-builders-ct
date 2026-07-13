# Release Report — Southern Suburbs Builders Website Template

## 1. Final status

Website built, merged, QA'd, and **deployed live**. Buyer package, product
pack, portfolio case study, blog article, and marketing assets are
complete. Francis Listing Manager import succeeded and was independently
verified. **The Etsy draft was not created** — two genuine blockers exist
(no active Etsy connection in this environment; price and Etsy taxonomy
unresolved) — both documented below rather than worked around or guessed.

## 2. Agent branches merged

`agent/claude-site`, `agent/grok-commerce`, `agent/codex-release` (all
local branches of the `ct-lead-gen` monorepo — see `handoff/FINAL-MERGE-PLAN.md`
for the foundational repo/branch mismatch found in preflight and how it
was resolved: a fresh clone of the standalone repo with content copied in,
rather than a literal cross-repo git merge).

## 3. Branch commit SHAs (source, in ct-lead-gen)

- `agent/claude-site`: `96cc3e6`
- `agent/grok-commerce`: `77dce95` (tip; 5 commits total)
- `agent/codex-release`: `0e89e52`

## 4. Conflicts resolved

Zero file-level conflicts between the three branches (disjoint path
ownership). One internal reconciliation: `agent/grok-commerce` contained
two divergent 7-day-campaign drafts (`handoff/grok/campaign/` and
`handoff/grok/growth/`) — the later, more complete `growth/` folder was
adopted as canonical. Full detail in `handoff/FINAL-MERGE-PLAN.md`.

## 5. Skills used

See `handoff/claude/SKILL-EXECUTION-PLAN.md` (build session) — accessibility,
security, SEO, and design practices, plus live browser QA via chrome-devtools
MCP tooling throughout this release for deployment verification, media
capture, and portfolio smoke-testing.

## 6. Website repository

`iederees-create/southern-suburbs-builders-ct`

## 7. Website final SHA

`e790ebd` (branch `main`)

## 8. Demo URL

https://iederees-create.github.io/southern-suburbs-builders-ct/

## 9. Demo verification result

**Pass.** Verified live (not from a local build) — see
`handoff/PUBLIC-DEMO-VERIFICATION.md`: all pages HTTP 200, custom 404
confirmed serving real content, Planner exercised live against the actual
deployed `site-config.js` (correct budget math), mobile nav confirmed
full-height with no horizontal overflow, corrected canonical/OG metadata
confirmed live.

## 10. Portfolio repository

`iederees-create/3D-Portfolio`

## 11. Portfolio final SHA

`2803963` (branch `main`)

## 12. Portfolio project route

`/work` → "Construction Website Template" card (featured, with gallery
showcase and technical case study)

## 13. Blog route

`/blog/construction-website-quote-planner/` — "How to Build a Construction
Website That Generates Better Quote Requests"

## 14. Buyer ZIP path

`seller-pack/buyer-files/01-SOUTHERN-SUBURBS-BUILDERS-TEMPLATE.zip`

## 15. Buyer-file list

1. `01-SOUTHERN-SUBURBS-BUILDERS-TEMPLATE.zip` — template source
2. `02-START-HERE.html`
3. `03-COMPLETE-BUYER-GUIDE.html`
4. `04-LICENSE.txt`
5. `05-AI-DISCLOSURE-AND-IMPORTANT-NOTICES.txt`

(exactly 5 — Etsy's buyer-file limit)

## 16. Product-pack path

`seller-pack/southern-suburbs-builders-complete-product-pack.zip`

## 17. Product-pack validation result

**Pass** — `validate-product-pack.js`, `validate-zip-content.js`,
`scan-secrets.js` all passed. See `seller-pack/PRODUCT-PACK-VALIDATION.md`
for the important schema-discrepancy finding: the real Francis Listing
Manager CLI import schema differs from Codex's documented schema (verified
by reading the actual FLM source, not the doc).

## 18. Listing-image paths

`seller-pack/media/listing-images/01-cover.png` through `10-included-files-buyer-guide.png`

## 19. Image count

10 (exactly)

## 20. Listing-video path

`seller-pack/media/video/etsy-listing-video.mp4` (13.5s, 1080x1080, MP4/H.264)

## 21. Portfolio-video paths

`public/projects/southern-suburbs-builders/preview.mp4` and `preview.webm`
(36s, 1080x1080) in the 3D-Portfolio repo, plus `video-poster.webp`

## 22. Product name

Southern Suburbs Builders Website Template

## 23. SKU

`BUILDERS-WEB-001` (internal name used for Francis Listing Manager import: "Southern Suburbs Builders Website Template")

## 24. Price

**Unresolved.** No price was found in any agent's output; none was guessed.
See `handoff/PHASE-9-PRICE-CATEGORY-RESOLUTION.md`.

## 25. Currency

**Unresolved.** Must match the connected Etsy shop's actual currency —
not determinable from this environment. Not assumed to be USD.

## 26. Category

Not set — deferred to Etsy's own taxonomy lookup, never invented.

## 27. Taxonomy

**Unresolved** — `etsy_taxonomy_id` is `null` in the imported Francis
Listing Manager record. Required before a draft can be created
(`validateProductForDraft` in `etsyDeploymentService.js`).

## 28. Francis Listing Manager product ID

**8** — created via `npm run product:import`, independently verified via
a direct read-back query (not just the CLI's success message): correct
internal_name, title, 13 tags, 10 images, 5 files, `price: 0` (correctly
unset, not guessed), `etsy_taxonomy_id: null`, `etsy_listing_id: null`.

## 29. Etsy draft ID

**None created.** `npm run etsy:draft -- --product-id 8` was run and
refused, exactly as designed:
```
Refusing to run: ETSY_API_ENABLED is not true. Enable and connect Etsy first.
```
This is a genuine environment blocker — no Etsy connection is configured
in this environment — independent of, and in addition to, the unresolved
price/taxonomy blocker (which `validateProductForDraft` would also have
refused on, separately, once an Etsy connection existed).

## 30. Etsy draft state

Not applicable — no draft exists.

## 31. Imported image count

10 (verified via direct database read-back)

## 32. Imported buyer-file count

5 (verified via direct database read-back)

## 33. Etsy video status

Not uploaded (no Etsy connection to upload through). The finished video
(`seller-pack/media/video/etsy-listing-video.mp4`) is preserved for manual
attachment once a human completes the Etsy draft — per the task's
instruction not to browser-automate Etsy or guess at video-upload API
support.

## 34. Campaign folder

`seller-pack/marketing/` (7-day-launch, 30-day-content, pinterest,
youtube, email, lead-magnet, community, buyer-support, analytics,
udemy-future-course) + `seller-pack/marketing/CAMPAIGN-INDEX.csv`

## 35. Lead-magnet folder

`seller-pack/marketing/lead-magnet/` — Construction Quote Readiness
Checklist (HTML, plain-text, social preview image); no email
signup/delivery system exists or is claimed — documented as future work.

## 36. Udemy future-course folder

`seller-pack/marketing/udemy-future-course/` — course pack preserved,
`README.md` marks MANUAL UDEMY COURSE CREATION AND UPLOAD REQUIRED.

## 37. Portfolio Etsy-link audit result

**Clean.** Independently re-verified (not just trusted from Codex's audit):
zero occurrences of `etsyUrl:` set and zero occurrences of the generic
`nextgenwebs.etsy.com` shop URL anywhere in `WorkPage.tsx`. New project
added with `etsyUrl` intentionally omitted. See
`handoff/PORTFOLIO-ETSY-LINK-RESOLUTION.md`.

## 38. Remaining warnings

- Lighthouse Cumulative Layout Shift scored 0.99/1 (displayValue 0.042) —
  within the "good" <0.1 threshold, not a real issue, noted for completeness.
- The portfolio repo has several unrelated untracked local files (a
  colleague's `.agents/`, `.claude/`, `skills-lock.json`, and ~14 video
  files) that were deliberately left untouched and were **not** committed
  as part of this release — they predate this session and are not this
  release's responsibility.

## 39. Remaining manual actions

1. **Confirm sale price and currency** for the Etsy listing (Phase 9 —
   see `handoff/PHASE-9-PRICE-CATEGORY-RESOLUTION.md`).
2. **Connect Etsy** in Francis Listing Manager (set `ETSY_API_ENABLED`
   and complete the OAuth connection) — currently not connected in this
   environment.
3. **Set the Etsy taxonomy ID** on product 8 via Francis Listing Manager's
   own taxonomy lookup once connected — never invented in this release.
4. Once price, currency, and taxonomy are set, run
   `npm run etsy:draft -- --product-id 8` (or use the web UI's "Create
   Complete Etsy Draft" button) to create the draft.
5. **Manually attach the Etsy listing video** (`etsy-listing-video.mp4`)
   to the draft if Etsy's video-upload API support cannot be confirmed as
   officially documented at that time.
6. Review the Etsy draft carefully in Francis Listing Manager's own
   read-back before considering publication.

## 40. Post-publication URL update instructions

**Review the Etsy draft carefully and publish it manually when satisfied.**

After manual publication:

1. Copy the exact public Etsy product URL.
2. Add it to the "Construction Website Template" project's `etsyUrl` field
   in `/home/iedrees/Workspace/3D-Portfolio/src/pages/WorkPage.tsx` (the
   only project entry this release added — do not touch any other
   project's `etsyUrl`).
3. Enable the "Buy on Etsy" CTA by virtue of that field now being set (the
   `ProjectCard` component already conditionally renders it —
   `{project.etsyUrl && (...)}` — no other code change needed).
4. Replace `EXACT_ETSY_PRODUCT_URL_PENDING_PUBLICATION` in
   `seller-pack/marketing/CAMPAIGN-INDEX.csv` (Day 7 row) with the real URL.
5. Add the URL to `seller-pack/marketing/pinterest/`, `youtube/`, and the
   relevant social campaign files wherever they currently reference the
   pending-URL placeholder.
6. Run `npm run build` in the 3D-Portfolio repo, smoke-test the updated
   card and CTA in a real browser, and redeploy.
