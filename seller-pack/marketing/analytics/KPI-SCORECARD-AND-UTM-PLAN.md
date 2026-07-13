# KPI Scorecard & UTM Plan — southern_suburbs_builders_launch

**Note:** No pre-existing KPI scorecard or UTM plan was found in
`handoff/codex/*` to finalise — Codex's branch delivered validation
tooling and audits, not a KPI/UTM document. This file is created fresh for
this release rather than left missing, using the campaign name specified
in the task brief.

## UTM structure

`utm_campaign=southern_suburbs_builders_launch`
`utm_medium={social|email|pinterest|youtube|blog}`
`utm_source={platform, e.g. instagram, facebook, pinterest, youtube, newsletter}`
`utm_content={day-1 ... day-7, or asset name}`

Example (live demo link, safe to use now):
```
https://iederees-create.github.io/southern-suburbs-builders-ct/?utm_campaign=southern_suburbs_builders_launch&utm_medium=social&utm_source=instagram&utm_content=day-1
```

**Do not apply UTM parameters to the Etsy product URL — it does not exist
yet.** Day 7's "Buy on Etsy" destination in `CAMPAIGN-INDEX.csv` remains
`EXACT_ETSY_PRODUCT_URL_PENDING_PUBLICATION` until manual publication; UTM
tagging for that link is a post-publication task (see the campaign index
and `seller-pack/RELEASE-REPORT.md`).

## KPI scorecard (targets to track post-launch, not pre-filled results)

| Metric | Where measured | Target (illustrative — set by business owner) |
|---|---|---|
| Live demo sessions | GitHub Pages / referrer tracking | Track via UTM `utm_content` per day |
| Planner completions (calculate clicks) | Not currently instrumented — no analytics script ships with the template by design (see FINAL-PRODUCT-FACTS.json: no tracking by default) | N/A until the business owner adds their own analytics |
| Etsy listing views/favourites | Etsy Shop Manager stats, post-publication | Post-publication only |
| Etsy conversion rate | Etsy Shop Manager stats, post-publication | Post-publication only |
| Portfolio case-study article views | 3D-Portfolio hosting analytics, if configured | Not currently instrumented |

**Honesty note:** the template deliberately ships with no analytics/tracking
script (a stated product fact — see `handoff/FINAL-PRODUCT-FACTS.json`).
This scorecard cannot report real numbers until the business owner adds
their own analytics to the demo/portfolio, which is outside this release's
scope. It is provided as a measurement plan, not fabricated results.
