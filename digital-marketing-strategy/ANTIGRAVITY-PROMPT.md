# Antigravity Prompt — Southern Suburbs Builders Digital Marketing Strategy

Copy everything inside the block below into Antigravity on the second computer.

---

```text
You are assisting with the Southern Suburbs Builders digital marketing strategy.

REPOSITORY
- GitHub: iederees-create/southern-suburbs-builders-ct
- Clone URL: https://github.com/iederees-create/southern-suburbs-builders-ct.git
- Required branch: work/digital-marketing-strategy

YOUR JOB
Help the user refine marketing strategy and campaign documents on this branch only.
Do not implement website features. Do not publish anything.

STEP 1 — LOCATE OR CLONE
1. If the repo is not present, clone it:
   git clone https://github.com/iederees-create/southern-suburbs-builders-ct.git
   cd southern-suburbs-builders-ct
2. If already cloned:
   cd southern-suburbs-builders-ct
   git fetch origin --prune

STEP 2 — CHECK OUT THE STRATEGY BRANCH
git switch --track origin/work/digital-marketing-strategy
# or if local branch exists:
git switch work/digital-marketing-strategy
git pull --ff-only origin work/digital-marketing-strategy

Confirm:
git branch --show-current
# must print: work/digital-marketing-strategy
git status --short

STEP 3 — READ THE COLLABORATION LAYER
Read in order:
1. digital-marketing-strategy/README.md
2. digital-marketing-strategy/STRATEGY-INDEX.md
3. digital-marketing-strategy/CURRENT-STATUS.md
4. digital-marketing-strategy/EDITING-RULES.md
5. digital-marketing-strategy/REVIEW-CHECKLIST.md

STEP 4 — INSPECT CANONICAL MARKETING MATERIAL
Inspect existing files under (only those that exist):
- handoff/grok/growth/
- handoff/grok/campaign/
- handoff/grok/blog/
- handoff/grok/ (listing, positioning, storyboards)
- handoff/codex/ (QA / portfolio plans — not a full content pack)
- seller-pack/drafts/
- handoff/FINAL-PRODUCT-FACTS.json if present

Prefer handoff/grok/growth/ over older campaign/ duplicates when editing.

Do not invent Codex marketing files that are missing (e.g. handoff/codex/marketing/*).

STEP 5 — ASK THE USER WHAT TO IMPROVE
Do not assume the work area. Ask which part they want to improve. Options include:
- seven-day campaign
- daily Facebook posts
- Instagram carousels
- LinkedIn posts
- X posts
- Pinterest pins
- YouTube scripts
- Grok Imagine prompts
- email sequence
- lead magnet
- portfolio conversion funnel
- SEO blog strategy
- Etsy listing conversion
- A/B testing
- KPI tracking
- Udemy course planning
- remote workspace docs (this folder)

STEP 6 — HARD CONSTRAINTS
- Make changes only on work/digital-marketing-strategy
- Do not edit website source (index.html, app.js, planner.js, style.css, etc.)
- Do not change the Renovation Scope & Budget Planner code
- Do not change Etsy integration code
- Do not publish Etsy or social content
- Do not schedule posts
- Do not create fake screenshots
- Do not invent ratings, reviews, customers, results, or sales
- Do not claim guaranteed leads or guaranteed estimates
- Do not create fake scarcity
- Preserve campaign narrative: From vague enquiries to build-ready leads
- Positioning: lead-generation and project-qualification system for builders — not merely a brochure website
- Etsy is the only marketplace
- Keep preliminary-estimate disclaimers
- Preserve pending placeholders until real values exist:
  EXACT_ETSY_PRODUCT_URL_PENDING_PUBLICATION
  UDEMY_COURSE_URL_PENDING
  PORTFOLIO_PROJECT_URL_PENDING
  BLOG_URL_PENDING
  (and LIVE_DEMO / ACTUAL_* media placeholders where used)
- Never use a generic Etsy shop homepage as if it were the exact product listing
- Days 1–6 can generally be prepared before Etsy publication
- Day 7 purchase messaging and Email 5 purchase CTA require the exact public Etsy product URL
- Etsy buttons stay hidden until the listing is public
- Udemy is future manual work and is not currently published
- Never merge main
- Never force-push unless the user explicitly instructs it

STEP 7 — EDIT
Make focused improvements to the chosen marketing docs.
Do not rewrite valid completed material merely to create activity.
Update digital-marketing-strategy/CHANGELOG.md when collaboration-layer behaviour changes.
Update CURRENT-STATUS.md if readiness changes.

STEP 8 — COMMIT AND PUSH (ONLY AFTER USER APPROVES)
Show the diff summary and ask for approval before committing.
Then:

git add digital-marketing-strategy handoff/grok handoff/codex seller-pack/drafts
git status --short
git commit -m "Refine Southern Suburbs Builders digital strategy"
git push origin work/digital-marketing-strategy

Report:
- commit SHA
- files changed
- branch name
- confirmation that main was not modified
- confirmation that nothing was published

If push is rejected, pull --ff-only and retry; do not force-push.

STEP 9 — PRODUCT FACTS
Use only product facts from existing handoff docs and FINAL-PRODUCT-FACTS.json.
Mark unverified features clearly. Do not invent finished planner fields, screenshots, or live URLs.
```

---

## Short reminder for the human

1. Open the cloned repo on branch `work/digital-marketing-strategy`  
2. Paste the prompt above into Antigravity  
3. Tell Antigravity which marketing area to refine  
