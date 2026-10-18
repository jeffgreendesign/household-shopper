# Household Shopper

Grok Bot template. Remembers your household's sizes, rooms, fixtures, stores, and memberships, then turns "new boots for Sam" into a short list of 2-3 options with a recommended size, fit confidence, whether it arrives by your deadline, total cost, and sources.

**It never buys.** It doesn't add to a cart or check out unless you explicitly ask, and then it hands off to Grok Bot's built-in shopping and purchase skills.

**Status:** paused experiment, v0.1.0. Instructions and skills were tested by hand against real product pages (Amazon, Target, a Shopify store) with fictional people only. Not tested end to end with a real household.

## What it does

- Remembers one dated fact per item ("Sam: shoes US kids 11 (kids system), foot 17.5 cm, as of 2026-10, recheck after 2027-04") and asks you to confirm stale ones.
- **Fit check** (`true-fit-check`): reads the size chart, fit notes, and review fit comments; gives a size and a confidence; never invents a chart or review.
- **Deadline check** (`deadline-delivery-check`): in the browser, with your ZIP set, keeps only options that are shown arriving in time. "Tomorrow" with no time window doesn't count for a time-of-day deadline. Guesses are labeled.
- Handles sized items, consumables, event food (allergy constraints as hard filters), fixtures and parts (exact spec match), furniture (room dimensions), and research requests.
- Mobile-friendly answers: top pick and confidence first, one line per option, totals and sources last.

## Optional: Shopify Catalog lookup

`shopify-catalog-lookup` can query Shopify's public Catalog endpoint for exact variant, stock, and price at Shopify stores. It's optional, read-only (search and product tools only, never cart, checkout, or orders), and **needs no key**. If it fails, the bot just browses.

Shopify's API License and Terms of Use apply to that endpoint. **They haven't been fully reviewed for this project.** Read them before enabling the skill. Anonymous throughput isn't guaranteed, and Shopify advises against unauthenticated production traffic.

## Install

1. Create a Grok Bot and paste `bot-instructions.md` as its instructions.
2. Add the skills in `skills/` (the Shopify one is optional).
3. Start a chat. Setup takes under 3 minutes, one question at a time, and you can skip it and shop right away.

## Privacy and safety

- Uses its own memory only. It reads shared memory only for who's who, and never writes sizes, allergies, health, or gift surprises there.
- Saves a fact only after you confirm. "What do you know about X" lists it; "forget X" removes it.
- Never messages, emails, or posts to anyone but you.
- No deal hunting, coupon sweeps, or homemade price tracking. No health or allergy advice beyond applying a constraint you stated.
- An optional monthly check (stale sizes, consumables due) is offered at setup, off by default, created only on a yes.

## Repo layout

- `bot-instructions.md`, `skills/`, `docs/DESIGN.md`, `docs/TESTING.md`, `tests/`.

## License

MIT. See `LICENSE`.
