---
name: best-buy-store-availability
description: Find Best Buy stores near a location and determine whether a SKU is available in one, joining the Stores and Products APIs the way the contract does not.
api: Best Buy Stores API
operations:
  - listStores
  - getStoreById
  - getProductBySku
generated: '2026-08-27'
method: generated
source: openapi/best-buy-stores-api-openapi.yml, openapi/best-buy-products-api-openapi.yml, data-model/best-buy-data-model.yml
---

# Best Buy store lookup and in-store availability

Base URL `https://api.bestbuy.com/v1`. `apiKey` in the query string, `format=json` always.

The Stores API and the Products API are **not joined in the contract** — there is no `$ref` between
them. The join happens at the application layer, on `storeId`. This skill is that join.

## Step 1 — find stores near a location

`listStores` with a filter expression in the path:

    GET /stores(area(55423,25))?apiKey=KEY&format=json

`area(postalCode, miles)` is the proximity filter. You can also filter on plain attributes:

    GET /stores(city=Minneapolis&state=MN)?apiKey=KEY&format=json&show=storeId,name,city,state,phone,distance,hours

Useful fields on `Store`: `storeId`, `name`, `longName`, `address`, `city`, `state`, `zipcode`,
`phone`, `lat`, `lng`, `distance`, `storeType`, `hours`, `gmtOffset`, `services[]`.

Filter on capability with `services`, e.g. stores offering a named service.

## Step 2 — read one store

    GET /stores/{storeId}?apiKey=KEY&format=json

404 means the storeId is unknown.

## Step 3 — check whether a SKU is in that store

Per-SKU near-real-time in-store availability was added in release R17.3 (2017-06-06) and is queried
by `storeId` **or** by `postalCode`. Reference:
https://bestbuyapis.github.io/api-documentation/#in-store-availability

Read `inStoreAvailability` and `onlineAvailability` off the product:

    GET /products/6354884?apiKey=KEY&format=json&show=sku,name,salePrice,inStoreAvailability,onlineAvailability

Do **not** rely on the deprecated text fields `inStoreAvailabilityText`,
`inStoreAvailabilityTextHtml`, `onlineAvailabilityText` or `onlineAvailabilityTextHtml` — Best Buy
flagged all four as stale in R17.4 (2017-10-01) and warned they may not match bestbuy.com.

## Rate budget for this flow

A "nearest store with this item" answer is **two** calls: one `listStores` with `area(...)`, one
product read. Do not iterate every returned store with its own request — at 5 req/sec a 25-store
radius will trip the QPS limit immediately and return 403 with no Retry-After.

Paging note: `StoreListResponse` carries `from`/`to`/`total`/`currentPage`/`totalPages` but **no**
`nextCursorMark`. Deep cursor paging is available on products and not on stores; use `page` and
`pageSize` here.
