---
name: best-buy-recommendations
description: Pull Best Buy trending, most-viewed, also-viewed and also-bought product signals and resolve them back to full catalog records.
api: Best Buy Recommendations API
operations:
  - getTrendingProducts
  - getMostViewedProducts
  - getAlsoViewedProducts
  - getAlsoBoughtProducts
  - getProductBySku
generated: '2026-08-27'
method: generated
source: openapi/best-buy-recommendations-api-openapi.yml, data-model/best-buy-data-model.yml
---

# Best Buy recommendations

Base URL `https://api.bestbuy.com/v1`. `apiKey` in the query string, `format=json`.

Four behaviour-derived signals. Two are category-scoped, two are SKU-scoped.

## Category-scoped

    GET /products/trendingViewed?apiKey=KEY&format=json          # getTrendingProducts
    GET /products/mostViewed?apiKey=KEY&format=json              # getMostViewedProducts

Both accept an optional category identifier to scope the list. Unscoped, they return the
site-wide list.

## SKU-scoped

    GET /products/{sku}/alsoViewed?apiKey=KEY&format=json        # getAlsoViewedProducts
    GET /products/{sku}/alsoBought?apiKey=KEY&format=json        # getAlsoBoughtProducts

`alsoViewed` is a browsing signal; `alsoBought` is a purchase signal. They answer different
questions — do not treat them as interchangeable. A 404 means the SKU is unknown or carries no
recommendation data.

## The response is NOT a Product

This is the trap in this API. Recommendations return `RecommendedProduct`, a **different, thinner**
schema from the catalog's `Product`, with pluralised containers:

| RecommendedProduct | Product |
|---|---|
| `sku` | `sku` |
| `names` (container) | `name` (scalar) |
| `images` (container) | `image` (scalar) |
| `prices` (container) | `regularPrice`, `salePrice`, `onSale` |
| `links` (container) | `url`, `addToCartUrl` |
| `rank` | — |

The envelope is different too: `RecommendationsResponse` is `{metadata, results}`, not the
`{from,to,total,currentPage,totalPages,...}` shape the catalog APIs use. Parse it separately.

## Step — resolve back to the catalog

If you need full product detail, join on `sku` — and batch the join rather than looping:

    GET /products(sku in(6354884,6354885,6354886))?apiKey=KEY&format=json&show=sku,name,salePrice,onlineAvailability

One recommendation call plus one batched catalog call is 2 requests. Looping a 10-item
recommendation list is 11 requests and will approach the 5 req/sec ceiling.

## Retired endpoint

`beta/products/{sku}/similar` was retired in R17.2 (2017-04-03) when its upstream data source was
deprecated. It permanently returns 404. Use `alsoViewed` or `alsoBought` instead.
