# Testing

Manual, read-only tests on 2026-10-17. Fictional subjects only (Sam, age 6, US kids 11; an adult with a 32 waist). Logged out, nothing saved to memory, no carts or messages.

## Fit check, per product page

| Page | Size chart | Reviews | Result |
|---|---|---|---|
| Amazon kids boot | Not readable without a browser (captcha) | Not read | Low-confidence guess |
| Target kids boot | Readable (chart fragment in page data) | Aggregate fit score readable ("true to size") | High confidence; flagged toddler vs kids sizing |
| Shopify brand belt | Readable size guide ("buy your pant size") | Review widget loads client-side; not read | Medium (capped) |
| Target men's belt | Readable (M = 32-36) | Not checked | Medium; edge-of-range case |

## Deadline check

"Brown belt by tomorrow 5pm" failed to confirm anywhere without a browser: the logged-out store list followed the server's IP rather than the ZIP, the fulfillment data was behind bot protection (not bypassed), and Amazon showed a captcha. A browser rerun later showed the deadline filter letting through a "tomorrow" promise with no time window and a delivery date seen for a different size. Both are now explicit rules.

## Shopify Catalog

The keyless Catalog endpoint worked: search, get_product, and lookup in about 0.4-0.8 s per call. Sizes in the query don't filter results; variants must be selected with get_product. No delivery dates are provided.

## Lessons

1. Amazon and ZIP-specific delivery need the browser.
2. Review widgets (Okendo, Yotpo, Bazaarvoice) often aren't in the HTML; say "reviews not read".
3. Store kids' sizes with the sizing system and foot length.
4. Belt sizing differs by brand; quote the brand's guide.

## Not yet done

An end-to-end run with the saved skills in a live bot, including the deadline test in a browser. Development is paused.
