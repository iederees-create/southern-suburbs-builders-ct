# Listing Disclosures — Southern Suburbs Builders Website Template

Required disclosures, each with the exact location it appears in the final
listing/product, for a pre-publication compliance check.

| Disclosure | Present in | Wording source |
|---|---|---|
| Digital download / no physical item | `final-description.txt` ("THIS IS A DIGITAL DOWNLOAD. No physical item ships.") and `LICENSE.txt` §6 | Verified against actual delivery method — genuinely a file download, no shipping |
| AI-assisted development | `final-description.txt` ("AI DISCLOSURE" section) and `05-AI-DISCLOSURE-AND-IMPORTANT-NOTICES.txt` in the buyer ZIP | Accurate — Claude Code (Anthropic) built the site/code, Grok (xAI) drafted commerce copy |
| Refund terms | `final-description.txt` ("REFUNDS") and `LICENSE.txt` §7 | Subject to Etsy digital-item policy + applicable law, not a custom refund guarantee |
| Preliminary-estimate / non-binding disclaimer | `final-description.txt`, `final-faq.md` Q2, the live site's `disclaimer.html`, and every Planner-generated summary | Verified directly against `planner.js`'s output text and `disclaimer.html` |
| Fictional demo content | `final-description.txt` ("FICTIONAL DEMO CONTENT"), `final-faq.md` Q15 | Verified against the live site's footer disclaimer and testimonial "(fictional)" tags |
| Licence scope (one end-client) | `final-description.txt` ("LICENCE"), `final-faq.md` Q10-11, `04-LICENSE.txt` | Set by the seller as standard practice consistent with the existing Westlake Pest Control template's licence terms in this shop |
| Support boundaries | `final-description.txt` ("SUPPORT"), `03-COMPLETE-BUYER-GUIDE.html` | Matches the support policy consolidated into the buyer ZIP |
| Hosting/domain not included | `final-description.txt` ("DEPLOYMENT"), `final-faq.md` Q5-6, `02-START-HERE.html` | Verified — this is a static file download with no hosting service attached |

## Not yet resolvable disclosures

- **Exact price and currency**: cannot be disclosed accurately until Phase 9
  resolves them (see `handoff/FINAL-MERGE-PLAN.md` placeholder classification
  and the price/currency section of this release's final report). The
  listing description intentionally does not state a numeric price.
- **Public Etsy product URL**: does not exist yet — the listing is a draft
  only. No file in this release states a live, clickable Etsy purchase URL.
