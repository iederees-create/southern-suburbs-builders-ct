# Digital Marketing Strategy — Remote Collaboration Workspace

**Repository:** [iederees-create/southern-suburbs-builders-ct](https://github.com/iederees-create/southern-suburbs-builders-ct)  
**Branch (required):** `work/digital-marketing-strategy`  
**Product:** Southern Suburbs Builders Website Template  
**Last workspace update:** 2026-07-13

---

## What this project is

This repository contains the **Southern Suburbs Builders** public demo site, buyer packaging, and multi-agent handoffs used to commercialise a construction-industry website template.

This folder (`digital-marketing-strategy/`) is the **navigation and collaboration layer** for remote editing (including Antigravity on a second PC). It does **not** replace the canonical strategy documents under `handoff/` and `seller-pack/`.

---

## What the product is

**Southern Suburbs Builders Website Template** — a responsive construction website template centred on an interactive **Renovation Scope & Budget Planner**.

The planner helps visitors define project scope and produce a structured quote brief with preliminary budget guidance.  
**It is not a binding construction quotation.**

---

## Campaign narrative

**From vague enquiries to build-ready leads.**

### Core positioning

Not merely a construction website.  
It is a **lead-generation and project-qualification system for builders.**

---

## What the marketing strategy is intended to achieve

1. Convert builders and renovation contractors who need better-quality enquiries  
2. Promote the live demo and portfolio case study  
3. Drive purchases via the **exact public Etsy product listing** (when available)  
4. Support SEO blog, social launch (7 days), email nurture, and future Udemy planning  
5. Keep claims honest: no guaranteed leads, no fake scarcity, preliminary estimates only  

### Main sales platform

**Etsy only** (exact product URL — never a generic shop homepage as the product link)

### Supporting channels

- 3D Portfolio  
- SEO blog  
- Facebook personal profile  
- Facebook business page  
- Instagram  
- LinkedIn  
- X  
- Pinterest  
- YouTube  
- Email marketing  
- Permitted online communities  
- Future Udemy course planning  

### Not in scope as marketplaces

Creem · Gumroad · Payhip · Shopify · WooCommerce · Lemon Squeezy · Creative Market · Envato · Creative Fabrica · Ko-fi · other marketplaces

---

## Where the strategy files live (canonical sources)

| Location | Role |
|---|---|
| `handoff/grok/growth/` | Primary Grok growth pack (Etsy, 7-day, social, email, Udemy plan, etc.) |
| `handoff/grok/campaign/` | Earlier 7-day creative campaign pack |
| `handoff/grok/blog/` | SEO blog article package |
| `handoff/grok/*.md` | Listing, positioning, portfolio case study, verify gates |
| `handoff/codex/` | QA, security, portfolio/Etsy link audits (not a full marketing content pack yet) |
| `seller-pack/drafts/` | Paste-ready listing draft mirrors |
| `handoff/FINAL-PRODUCT-FACTS.json` | Integrated product facts when present |
| `digital-marketing-strategy/` | **This folder** — index, status, remote setup, Antigravity prompt |

**Do not duplicate entire strategy packs into this folder.** Edit canonical files; keep this folder as the map.

---

## Branch rules

| Do | Don’t |
|---|---|
| Work on `work/digital-marketing-strategy` | Edit/merge `main` from the second PC |
| Push only to `origin/work/digital-marketing-strategy` | Force-push unless explicitly instructed |
| Edit marketing strategy docs | Edit website source (`index.html`, `app.js`, `planner.js`, etc.) |

---

## Which files to edit first

1. Read **this README**  
2. Read `STRATEGY-INDEX.md` (map to canonical files)  
3. Read `CURRENT-STATUS.md` and `EDITING-RULES.md`  
4. Then open the specific pack you want to improve (see index groups)

Recommended starting points by goal:

| Goal | Start here |
|---|---|
| 7-day launch | `handoff/grok/growth/7-DAY-LAUNCH-CAMPAIGN.md` + `DAY-0x.md` |
| Etsy conversion | `handoff/grok/growth/ETSY-CONVERSION-PACK.md` |
| Portfolio funnel | `handoff/grok/growth/PORTFOLIO-CONVERSION-PACK.md` |
| SEO blog | `handoff/grok/blog/` + `SEO-CONTENT-FUNNEL.md` |
| Email / lead magnet | `LEAD-MAGNET-PACK.md` + `EMAIL-SEQUENCE.md` |
| Udemy (future) | `UDEMY-COURSE-PACK.md` |

---

## How to save and push changes

```bash
git status --short
git branch --show-current   # must be work/digital-marketing-strategy

git add digital-marketing-strategy handoff/grok handoff/codex seller-pack/drafts
# only stage marketing docs you intentionally changed

git commit -m "Refine Southern Suburbs Builders digital strategy"
git push origin work/digital-marketing-strategy
```

See `REMOTE-PC-SETUP.md` for clone/switch commands on a second computer.

---

## What must not be changed

- Website source and planner implementation  
- Etsy integration / Francis automation from this branch’s marketing work  
- Publishing or scheduling social/Etsy content  
- Inventing screenshots, ratings, reviews, sales results  
- Replacing exact Etsy product URL with a generic shop homepage  
- Merging this branch into `main` without explicit instruction  

---

## Related docs in this folder

| File | Purpose |
|---|---|
| `STRATEGY-INDEX.md` | Links to all existing marketing sources |
| `CURRENT-STATUS.md` | What is ready vs pending |
| `EDITING-RULES.md` | Hard rules for editors |
| `REMOTE-PC-SETUP.md` | Second-PC git commands |
| `ANTIGRAVITY-PROMPT.md` | Paste-ready agent prompt |
| `REVIEW-CHECKLIST.md` | Pre-commit quality checks |
| `CHANGELOG.md` | Workspace changelog |
