# Best Buy GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the Best Buy API. Best Buy provides a REST-based Open API covering products, stores, categories, recommendations, open box items, and commerce operations. This GraphQL schema represents the same domain model as a typed, queryable graph — enabling clients to fetch exactly the product, store, pricing, and availability data they need in a single request rather than multiple REST calls.

The underlying data sources are documented at https://bestbuyapis.github.io/api-documentation/ and the GitHub organization is at https://github.com/BestBuyAPIs.

## Schema Source

This is a conceptual schema derived from the Best Buy Open API documentation. It is not an officially published GraphQL endpoint from Best Buy.

## Domain Coverage

The schema covers the following domains from the Best Buy API:

**Products** — Over one million current and historical products with real-time pricing, specifications, images, customer reviews, and category placement. Products are queryable by SKU, keyword, or category filter.

**Categories** — Best Buy's product taxonomy with 4,328+ categories arranged in a hierarchical tree from top-level department down to specific product types.

**Stores** — 1,587+ physical Best Buy locations across the United States and Puerto Rico with hours, addresses, services, and in-store availability data.

**Pricing** — Regular, sale, list, online, and in-store pricing variants with promotion and daily/weekly deal overlays.

**Availability** — Real-time in-store, online, ship-to-home, and ship-to-store availability by SKU and store location.

**Reviews and Ratings** — Customer-submitted reviews with author profiles, star ratings, and review metadata.

**Recommendations** — Trending, most-viewed, also-viewed, also-bought, and viewed-ultimately-bought recommendation signals by category or SKU.

**Open Box and Refurbished** — Discounted open box and Geek Squad certified refurbished items with condition ratings updated every five minutes.

**Commerce** — Cart management, shipping options, delivery estimates, and order creation for authorized partners.

**Membership and Rewards** — Best Buy Plus membership, renewal details, gift cards, rewards certificates, and promotional offers.

**Protection and Services** — Geek Squad protection plans, device trade-in, gift wrapping, and financing options.

## Root Query Fields

| Field | Return Type | Description |
|---|---|---|
| `product(sku: ID!)` | `Product` | Fetch a single product by SKU |
| `products(query: ProductQuery)` | `[Product]` | Search or filter products |
| `category(id: ID!)` | `ProductCategory` | Fetch a category by ID |
| `categories(parentId: ID)` | `[ProductCategory]` | Browse category tree |
| `store(id: ID!)` | `Store` | Fetch a single store by ID |
| `stores(query: StoreQuery)` | `[Store]` | Search stores by location or area |
| `recommendations(type: RecommendationType!, sku: ID, categoryId: ID)` | `[Product]` | Fetch recommendation lists |
| `openBoxItems(sku: ID, skus: [ID!], categoryId: ID)` | `[OpenBoxItem]` | Fetch open box / refurbished items |
| `deals(type: DealType)` | `[Promotion]` | Fetch current daily deals and door busters |
| `apiKey(key: String!)` | `APIKey` | Validate and inspect an API key |

## Type Summary

The schema defines 63 named types covering products, categories, stores, pricing, availability, reviews, commerce, membership, and API access control. See `best-buy-schema.graphql` for the full type definitions.
