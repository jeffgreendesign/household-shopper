# Design

Name ideas: **Fit & Fetch**, **House Sizes**, **Household Shopper** (clearest; my pick).

## Description (~40 words)
Remembers your household's sizes, rooms, fixtures, stores, and memberships, then turns "new boots for Sam" into a 2-3 option short list with a recommended size, delivery date, total cost, and sources. Never buys without your explicit go-ahead.

## Skills (outline, keep short)
1. **household-shopper-getting-started** (gettingStarted): one question at a time: who's in the household (name + age band only); favorite stores; memberships; ZIP for pickup/delivery; optionally one known size or fixture. Confirm, save, then offer a sample request.
2. **true-fit-check**: inputs = product URL + subject's stored size. Browser for Amazon. Read size chart, fit notes, page metadata, Target's fit score if present, then review fit mentions (count "runs small/large/true"). Match on sizing system and foot length for kids; apply the edge-of-range size-up rule for belts and growing kids and state it. Output size + confidence + up to 3 evidence links/quotes. Note when the review widget didn't load.
3. **deadline-delivery-check**: inputs = item + deadline + ZIP + memberships. Browser required. Set ZIP (and pickup store) on the site first, then read the delivery promise, compare pickup stock nearby, drop misses, label guesses.

## Routine (optional, offered at end of setup, off by default)
`monthly-household-check`, `0 9 1 * *`: list facts past their recheck date and consumables due by cadence in the next 2 weeks. If none, send nothing. Result goes only to the owner.

## Example memory (fictional)
- Example (fictional, delete after setup): `Sam (fictional example, age 6): shoes US kids 11 (kids system), foot 17.5 cm, as of 2026-10, recheck after 2027-04`.
- Defaults: recheck windows above; deadline = hard filter; save only after confirm.

## Flags
- **Review widgets are unreliable.** Bazaarvoice, Yotpo, PowerReviews, and Amazon reviews often load lazily, sit in iframes, paginate, or require sign-in. Static fetch usually misses them; the browser does better but is slow and may get blocked. Plan: try the page, then the vendor's public review page; if neither loads, say "reviews not read" and cap confidence at medium. Test on 3 PDPs from different platforms (Amazon, Target, a Shopify brand).
- **Overlap with Deal Hunting:** that template is about finding the lowest price and deals. This one is about fit, the right item for a known person/room, and the deadline. Keep the line clear: no coupon hunting or price-comparison sweeps here; hand "cheapest anywhere" to Deal Hunting or the built-in alerts. I haven't opened that template's contents, so check its skills for overlap.
- Delivery dates vary by ZIP and sign-in; a logged-out page may show a different promise. Always label which one you saw.

## Revision 2026-10-17 (from TEST-RESULTS.md)
- Browser required for Amazon and all delivery/pickup checks, ZIP/store set first.
- Kids' sizes stored with sizing system + foot length.
- Edge-of-range size-up for belts and growing kids, stated in the answer.
- Target fit score counts as review evidence.

The current instructions are in `../bot-instructions.md`; this file keeps the reasoning.

## Review findings (UX + agent review) and fixes

The review rated the first draft not shippable. All P0 and P1 items are fixed in v0.1.0:

- P0: skills created and referenced; "tomorrow" with no time window can't meet a time-of-day deadline; delivery re-checked for the recommended size variant; top pick leads with confidence, with separate Fit and Arrives labels.
- P1: edge-of-range rule corrected (pick the range containing the size; size up only at the top value, for belts and growing kids; follow a brand's pant-size guide); request types for consumables, event food, fixtures, furniture, and research; cold start asks only size and ZIP; store/time budget announced up front; mobile layout; memory verbs (list, forget, show saved fact); failure states (retry once, then skip; nothing meets the deadline; logged-out view).
- P2: "tax not shown" totals; "reviews not read" caps confidence at medium; memberships stored as "owner said"; built-in shopping skill handles carts.
