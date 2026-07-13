# Portfolio Etsy Link Resolution — Phase 12

## Independent verification of Codex's audit

Codex's `handoff/codex/PORTFOLIO-ETSY-LINK-AUDIT.md` found zero
project-level `etsyUrl` values set anywhere in `WorkPage.tsx`, and no use
of the generic `nextgenwebs.etsy.com` shop URL as a project purchase CTA.

I independently re-verified this before adding the new project entry:

```
$ grep -n "nextgenwebs.etsy.com" src/pages/WorkPage.tsx
(no matches)

$ grep -c "etsyUrl:" src/pages/WorkPage.tsx
0
```

**Confirmed clean.** No project in the portfolio currently has a live
purchase button pointing at a draft listing, a generic shop root, or an
unverified URL. Every project that could plausibly be a sellable Etsy
template has its `etsyUrl` either omitted entirely or explicitly commented
out with a reference to the audit (e.g. `// etsyUrl removed - see
PORTFOLIO-ETSY-LINK-AUDIT.md`).

## New project added this release

"Construction Website Template" was added to `WorkPage.tsx` with:
- `liveUrl: 'https://iederees-create.github.io/southern-suburbs-builders-ct/'`
- **no `etsyUrl`** (intentionally omitted, with an inline comment explaining why, matching the established convention used for every other draft-stage template in this file)

This keeps the "Buy Template" button hidden for this project (the
`ProjectCard` component only renders the Etsy CTA `{project.etsyUrl && (...)}`
when the field is present) until a human manually publishes the Etsy
listing and the exact URL is added per
`handoff/codex/PORTFOLIO-UPDATE-PLAN.md`'s post-publication procedure.

## No unrelated changes made

Per the task's instruction not to make unrelated design changes to
existing portfolio projects, this release touched only:
- One new object appended to the `projects` array in `WorkPage.tsx`
- One new media directory: `public/projects/southern-suburbs-builders/`

No existing project entries, components, or styles were modified.

## Remaining action (post-publication, per PORTFOLIO-UPDATE-PLAN.md)

1. Verify publication state in Francis Listing Manager.
2. Record the exact active Etsy listing URL.
3. Add `etsyUrl: '<exact listing URL>'` to the "Construction Website
   Template" project entry only.
4. Never use `https://nextgenwebs.etsy.com` (or any other generic shop
   root) as a project-level purchase URL.
5. Rebuild and redeploy the portfolio after making that one-line change.
