# Final Merge Plan — Southern Suburbs Builders Release

## Foundational finding (read this first)

The task brief assumed `/home/iedrees/Workspace/ct-lead-gen/clients/southern-suburbs-builders`
was a clone of `iederees-create/southern-suburbs-builders-ct` with the three
agent branches ready to merge into it. Preflight found this was not the case:

- That local path is **not a git repository**. It is two files
  (`index.html`, `style.css`) tracked as part of the much larger
  `ct-lead-gen` monorepo.
- `iederees-create/southern-suburbs-builders-ct` **does** exist on GitHub
  with Pages already serving it — but its `main` branch contains only the
  same old two files, from a single commit dated 2026-04-28
  ("Launch: Southern Suburbs Builders - Cape Town Ecosystem"), pre-dating
  the three-agent rebuild entirely.
- All three agent branches are real, pushed, and inspectable — but to
  **`ct-lead-gen`'s** `origin`, not to `southern-suburbs-builders-ct`. They
  share no git history with the standalone repo.

**Resolution (confirmed with the human owner before any repo action):**
fresh-clone `southern-suburbs-builders-ct` to a clean location
(`/home/iedrees/Workspace/release-build/southern-suburbs-builders-ct`),
branch `release/southern-suburbs-builders` from its `main`, and copy in the
finished, verified content from each agent's work rather than performing a
literal cross-repo `git merge --allow-unrelated-histories` (which would have
imported the entire unrelated `ct-lead-gen` monorepo history — 58+ other
client sites, lead CSVs, scripts — into what must stay a small, clean,
buyer-facing template repo). This matches the project's own established
pattern (see `ct-lead-gen/RELEASE-WORKFLOW.md` and `ct-lead-gen/CLAUDE.md`):
build in the monorepo, then publish a clean standalone demo repo.

## Branches inspected

| Branch | Commits (oldest→newest) | Files changed | Agent responsibility |
|---|---|---|---|
| `agent/claude-site` | `96cc3e6` Build premium construction template and renovation planner | 17 files, all under `clients/southern-suburbs-builders-claude/` | Website implementation: HTML/CSS/JS, planner engine + tests, legal pages, SEO assets, handoff docs |
| `agent/grok-commerce` | `7c2d270` → `4d4502e` → `3d48705` → `3510701` → `77dce95` (5 commits) | 62 files under `handoff/grok/*` and `seller-pack/drafts/*` | Marketing/commerce copy: Etsy listing strategy, 7-day campaign (two passes — see below), SEO blog package, growth/social packs, buyer onboarding drafts |
| `agent/codex-release` | `0e89e52` Add release validation and portfolio audit tooling | 12 files under `handoff/codex/*`, `scripts/release/*`, `tests/release/*` | QA/validation tooling: baseline audit, security review, release test matrix, product-pack schema notes, portfolio Etsy-link audit, validator scripts |

Fetched via `git fetch origin --prune` against `ct-lead-gen`'s origin before
inspection; `git log --oneline main..<branch>` was used on each to confirm
the full commit list (not just the first commit) per the task's instruction
not to assume a single commit contains all the work — this caught the fact
that `agent/grok-commerce` has 5 commits, not 1.

## File-overlap / conflict analysis

`comm -12` was run pairwise across the three branches' changed-file lists.
**Zero files are touched by more than one branch.** This is expected given
each agent owned a disjoint path prefix (`clients/southern-suburbs-builders-claude/`
vs `handoff/grok/` + `seller-pack/drafts/` vs `handoff/codex/` +
`scripts/release/` + `tests/release/`). There is no line-level merge
conflict to resolve between the three branches themselves.

## Internal reconciliation issue found within `agent/grok-commerce`

Grok's branch contains **two divergent passes** at the 7-day campaign
concept, written in two different commits:

- `handoff/grok/campaign/` (commit `3d48705`, "Add seven-day construction
  template creative campaign") — an earlier, narrower pass: 7 daily files
  plus a handful of supporting docs, structured around a 3-act narrative.
- `handoff/grok/growth/` (commit `77dce95`, "Add Etsy portfolio social and
  Udemy growth campaign") — the **latest** commit on the branch, explicitly
  self-described in `GROWTH-HANDOFF.md` as "Growth marketing package
  complete," and comprehensively covering every single item enumerated in
  this release task's "Expected GROK Handoff" list (Etsy conversion pack,
  SEO funnel, 7-day daily creative, Imagine prompts, short-video scripts,
  carousel/story copy, Pinterest, YouTube, social content bank, lead magnet,
  email sequence, portfolio conversion, buyer onboarding, support replies,
  community outreach, A/B test plan, Udemy course pack, growth handoff).

A diff of `DAY-01.md` between the two folders confirms they are genuinely
different drafts, not duplicates (different headline structure, different
word choices, the `campaign/` version additionally carries an explicit
"Publish gate: Safe before Etsy publication" annotation).

**Decision: `handoff/grok/growth/` is treated as the canonical, final
version.** `handoff/grok/campaign/` is retained in the repository for
provenance/history but is documented here as a superseded earlier draft —
Phase 8 (Etsy copy) and Phase 14 (marketing finalisation) source from
`growth/`, not `campaign/`.

## Merge order (as executed)

1. **`agent/claude-site`** — copied the complete, tested website
   (`clients/southern-suburbs-builders-claude/*`) to the repo root of the
   fresh standalone clone, replacing the old two-file demo. This is the
   **factual source of truth** for every product claim used downstream.
2. **`agent/grok-commerce`** — copied `handoff/grok/*` and
   `seller-pack/drafts/*` verbatim for later fact-checking (Phase 3) before
   any of its marketing copy is used in the public listing or blog.
3. **`agent/codex-release`** — copied `handoff/codex/*`, `scripts/release/*`,
   and `tests/release/*` verbatim; these are the validation tools and known
   risks used to drive Phase 4 (website QA) and later product-pack/media
   validation.

## Validation required after merge

- Re-run `npm test` (planner unit tests) and a syntax check on all JS from
  the copied website in its new location.
- Run `scripts/release/scan-secrets.js`, `validate-media.js`,
  `validate-product-pack.js`, `validate-zip-content.js` (from
  `agent/codex-release`) once the relevant artifacts exist.
- Cross-check every factual claim in `handoff/grok/growth/ETSY-CONVERSION-PACK.md`
  and `handoff/grok/etsy-listing-copy.md` against the live implementation
  before it is used in `seller-pack/listing/*` (Phase 3 / Phase 8).
- Confirm no file under `handoff/grok/` or `seller-pack/drafts/` references
  a live Etsy URL, published status, or fabricated statistic.
