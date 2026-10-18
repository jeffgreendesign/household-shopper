---
name: shopify-catalog-lookup
description: >-
  Optional, read-only: use before browsing when a Shopify store might carry the
  item, to get the exact variant, stock, price and product link. Not for fit or
  delivery dates.
---
# Shopify Catalog lookup (optional)
Endpoint: POST https://catalog.shopify.com/api/ucp/mcp (JSON-RPC, tools/call), no key needed.
Every call includes `meta.ucp-agent.profile` = the owner's agent profile URL if one is set in memory, otherwise Shopify's example profile https://shopify.dev/ucp/agent-profiles/examples/2026-08-25/valid-with-capabilities.json. Read-only tools only: search_catalog, get_product, lookup_catalog. Never use cart, checkout, or order tools.

1. Call `search_catalog` {catalog:{query}}. Sizes in the query don't filter results.
2. Pick 2-3 results and call `get_product` {catalog:{id}} first. Read `options` to find the store's exact size option name (for example "Accessory size"). Call again with `selected:[{name:<exact>,label:<size>}]`.
3. Record the variant id, `availability.available`, price, list_price, seller and product page `url`. Label it "Shopify Catalog said in stock at $X". Shipping text in the description is the merchant's own copy; label it that way.
4. Fit: pass the product page and any size chart in the description to true-fit-check.
5. Deadline: Catalog has no delivery dates. Run deadline-delivery-check in the browser.
6. On an error or rate limit, retry once, then fall back to browsing. Keyless throughput isn't guaranteed.
Never buy. Share the product page or checkout link only when the owner asks.
