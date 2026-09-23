---
name: best-buy-product-lookup
description: Look up Best Buy products by SKU or keyword and read back price, availability and review data without tripping the 5 requests-per-second ceiling.
api: Best Buy Products API
operations:
  - listProducts
  - getProductBySku
generated: '2026-08-27'
method: generated
source: openapi/best-buy-products-api-openapi.yml, conventions/best-buy-conventions.yml, rate-limits/best-buy-rate-limits.yml
---

# Best Buy product lookup

Base URL `https://api.bestbuy.com/v1`. Every request needs `apiKey` in the **query string** and
`format=json` — the historical default is XML, and forgetting `format=json` is the most common
first failure.

## Before you start

- Budget: **5 requests/second, 50,000 requests/day** per key. There are no rate-limit headers, so
  count your own calls.
- Exhaustion returns **403**, the same status as a bad key. If your key worked a moment ago, a 403
  means you are going too fast.
- Terms forbid caching returned content beyond **72 hours**, and response links expire after 7 days.

## Step 1 — one product by SKU

Use `getProductBySku`:

    GET /products/{sku}?apiKey=KEY&format=json

Trim the payload with `show`:

    GET /products/6354884?apiKey=KEY&format=json&show=sku,name,salePrice,regularPrice,onSale,onlineAvailability,inStoreAvailability,customerReviewAverage,customerReviewCount

A 404 here means the SKU is unknown. Note SKUs migrated from 10 digits to 7 digits in 2017 — never
validate a SKU by its length.

## Step 2 — many products in ONE call

Do **not** loop `getProductBySku`. Use `listProducts` with the `in(...)` operator, which the
documentation recommends specifically to avoid QPS errors:

    GET /products(sku in(6354884,6354885,6354886))?apiKey=KEY&format=json&show=sku,name,salePrice

This is the difference between 1 request and 3, and at scale between staying inside the daily
quota and burning it.

## Step 3 — search and filter

Filters live inside parentheses in the **path**, not as ordinary query parameters:

    GET /products(search=laptop&salePrice<800&manufacturer=lenovo)?apiKey=KEY&format=json&sort=salePrice.asc&pageSize=100

Operators: `=`, `!=`, `<`, `>`, `<=`, `>=`, `in(...)`.

## Step 4 — page the result set

Read the envelope: `total`, `currentPage`, `totalPages`, `from`, `to`.

- Shallow paging: `page=2&pageSize=100` (100 is the cap).
- Deep paging: take `nextCursorMark` from the response and pass it back as `cursorMark`. Stop when
  `nextCursorMark` stops changing.

## Error handling

| Status | What it means | What to do |
|---|---|---|
| 400 | Malformed filter or value. Unknown parameter *names* are ignored, so it is the expression, not the spelling | Fix the filter expression |
| 403 | Bad key **or** quota exhausted — indistinguishable | If the key is good, back off exponentially. No Retry-After is sent |
| 404 | Unknown SKU, or a retired endpoint | Verify the SKU |
| 405 | You used a non-GET method | The catalog surface is GET-only |
| 500/501/503 | Best Buy-side error | Retry with backoff; there is no status page to check |

Error bodies are `{"errorCode":"403","errorMessage":"..."}` — `errorCode` is a **string**, and the
OpenAPI's declared `{status,error,message}` shape and its `401` response do not match the wire.
There is no request-id in any response, so you cannot quote a failure by identifier to support.
