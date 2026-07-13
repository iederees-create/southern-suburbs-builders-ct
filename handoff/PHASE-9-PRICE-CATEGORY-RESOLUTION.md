# Phase 9 — Price, Category & Currency Resolution

## Price

**Status: UNRESOLVED.** Searched every file across all three merged agent
branches (`handoff/grok/*`, `seller-pack/drafts/*`, and the earlier
`etsy-ready-packages/southern-suburbs-builders-Website-Template.zip`
legacy listing) for a numeric price recommendation. None exists — every
occurrence in Grok's commerce copy is the literal placeholder string
`CONFIRMED_PRICE_PENDING`. Grok's own `BUILD-FACTS-TO-VERIFY.md` row I8
explicitly marks price/currency confirmation "NOT THIS AGENT" — i.e. Grok's
own brief scoped this to a human/Francis Listing Manager decision, not an
agent guess.

No price is stated anywhere in `seller-pack/listing/final-description.txt`
or any other file produced in this release.

## Currency

**Status: UNRESOLVED.** The Etsy shop's actual configured currency is not
determinable from any file in this repository or from the local
environment — it requires either an authenticated Francis Listing Manager
session (which can read the connected shop's settings) or direct knowledge
from the human shop owner. The Renovation Scope & Budget Planner's own
*demo* currency (ZAR) is an unrelated, independent fact — it is the
in-product default for the fictional demo business's illustrative rate
bands, not a signal about what currency the Etsy shop itself sells in. This
release does not conflate the two.

## Category / taxonomy

Deferred to Phase 10/17 — Francis Listing Manager's own taxonomy lookup
will be used at import time rather than guessing or inventing a numeric
Etsy taxonomy ID here.

## Action taken per the release brief's explicit instruction

> "If the price remains unresolved: import the product into Francis
> Listing Manager, preserve the media and buyer files, stop before creating
> the Etsy draft, clearly report that a price must be confirmed."

This release proceeds to Phase 10 (build the Complete Product Pack) and
Phase 17 (attempt the Francis Listing Manager import) with price and
currency fields explicitly left blank/flagged in the pack manifest — never
filled with a guessed number or an assumed USD default. Phase 18 (Etsy
draft creation) is not attempted while this remains unresolved; see
`seller-pack/RELEASE-REPORT.md` for the final status of that stop point.

**Required human action:** confirm the intended sale price and the Etsy
shop's actual selling currency before the Etsy draft step can be completed.
