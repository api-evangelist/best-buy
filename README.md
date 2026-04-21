# Best Buy (best-buy)
Best Buy is a multinational consumer electronics retailer offering technology products, services, and solutions through stores, online, and in-home consultations. Best Buy provides a developer API giving access to product data, store locations, categories, recommendations, open box offers, and commerce capabilities for partners and developers building retail integrations and applications.

**URL:** [https://developer.bestbuy.com](https://developer.bestbuy.com)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Retail, Consumer Electronics, E-Commerce, Products, Stores

## Timestamps

- **Created:** 2026-04-19
- **Modified:** 2026-04-19

## APIs

### Best Buy Products API
Access over one million current and historical Best Buy products with real-time pricing, availability, specifications, images, customer reviews, and categorization data. Supports detailed queries by SKU, keyword search, and filtering across all product attributes.

**Human URL:** [https://bestbuyapis.github.io/api-documentation/#products-api](https://bestbuyapis.github.io/api-documentation/#products-api)

#### Tags:

 - Products, Retail, Electronics, Pricing, Inventory

#### Properties

- [Documentation](https://bestbuyapis.github.io/api-documentation/#products-api)
- [OpenAPI](openapi/best-buy-products-api.yaml)

### Best Buy Stores API
Retrieve comprehensive store location and operational data for 1,587+ Best Buy locations across the United States and Puerto Rico. Supports area-based searches by postal code or latitude/longitude, store hours, services, and in-store product availability.

**Human URL:** [https://bestbuyapis.github.io/api-documentation/#stores-api](https://bestbuyapis.github.io/api-documentation/#stores-api)

#### Tags:

 - Stores, Locations, Retail, Geolocation

#### Properties

- [Documentation](https://bestbuyapis.github.io/api-documentation/#stores-api)
- [OpenAPI](openapi/best-buy-stores-api.yaml)

### Best Buy Categories API
Navigate Best Buy's product taxonomy with access to 4,328+ product categories. Browse hierarchical category paths from root to specific categories and integrate with product searches for category-specific filtering.

**Human URL:** [https://bestbuyapis.github.io/api-documentation/#categories-api](https://bestbuyapis.github.io/api-documentation/#categories-api)

#### Tags:

 - Categories, Taxonomy, Products

#### Properties

- [Documentation](https://bestbuyapis.github.io/api-documentation/#categories-api)

### Best Buy Recommendations API
Leverage customer behavior data to surface relevant products through trending products, most viewed, also viewed, also bought, and viewed-ultimately-bought recommendation types. Supports queries by category ID or specific SKU.

**Human URL:** [https://bestbuyapis.github.io/api-documentation/#recommendations-api](https://bestbuyapis.github.io/api-documentation/#recommendations-api)

#### Tags:

 - Recommendations, Personalization, Products

#### Properties

- [Documentation](https://bestbuyapis.github.io/api-documentation/#recommendations-api)
- [OpenAPI](openapi/best-buy-recommendations-api.yaml)

### Best Buy Buying Options (Open Box) API
Access discounted open box and Geek Squad certified refurbished merchandise with ship-from-store fulfillment. Supports single SKU, batch queries up to 100 SKUs, and category-based discovery with condition ratings updated every 5 minutes.

**Human URL:** [https://bestbuyapis.github.io/api-documentation/#buying-options-api](https://bestbuyapis.github.io/api-documentation/#buying-options-api)

#### Tags:

 - Open Box, Refurbished, Discounts, Products

#### Properties

- [Documentation](https://bestbuyapis.github.io/api-documentation/#buying-options-api)

### Best Buy Commerce API
Enable integrated shopping experiences for authorized partners with product availability lookups, shipping cost calculations, and order creation supporting store pickup, ship-to-home, and home delivery fulfillment options.

**Human URL:** [https://bestbuyapis.github.io/api-documentation/#commerce-api](https://bestbuyapis.github.io/api-documentation/#commerce-api)

#### Tags:

 - Commerce, Orders, Fulfillment, Partners

#### Properties

- [Documentation](https://bestbuyapis.github.io/api-documentation/#commerce-api)

## Common Properties

- [Website](https://www.bestbuy.com)
- [DeveloperPortal](https://developer.bestbuy.com)
- [Documentation](https://bestbuyapis.github.io/api-documentation/)
- [GettingStarted](https://bestbuyapis.github.io/api-documentation/#user-guide)
- [Authentication](https://bestbuyapis.github.io/api-documentation/#authorization)
- [SignUp](https://developer.bestbuy.com)
- [GitHubOrganization](https://github.com/BestBuyAPIs)
- [GitHubRepository](https://github.com/BestBuyAPIs/api-documentation)
- [RateLimits](https://bestbuyapis.github.io/api-documentation/#rate-limiting)
- [SpectralRules](rules/best-buy-spectral-rules.yml)
- [NaftikoCapability](capabilities/retail-discovery.yaml)
- [Vocabulary](vocabulary/best-buy-vocabulary.yaml)

## Features

| Name | Description |
|------|-------------|
| Products API | Access to over one million products with real-time pricing, availability, and specifications. |
| Stores API | Comprehensive data for 1,587+ US Best Buy locations including hours, services, and proximity search. |
| Categories API | Navigate 4,328+ product categories with hierarchical taxonomy browsing. |
| Recommendations API | Customer behavior-powered recommendations including trending, most viewed, also viewed, and also bought. |
| Open Box API | Discounted open box and certified refurbished merchandise with condition ratings and availability. |
| Commerce API | Partner-level shopping integration with order creation and fulfillment management. |
| Query Builder | Interactive tool for constructing API queries without starting from scratch. |
| JSON and XML Responses | Flexible response format support with JSON and XML output options. |
| Pagination and Cursors | Page-based and cursor-mark pagination for large product datasets. |
| Faceted Search | Summary aggregations by specified attributes with count limits for faceted browsing. |

## Use Cases

| Name | Description |
|------|-------------|
| Product Discovery | Full-text search and filtering across product descriptions, specifications, and reviews. |
| Inventory Management | Real-time in-store availability checking by postal code or store ID. |
| Recommendation Widgets | Display trending, most-viewed, and also-bought products on product detail pages. |
| Store Locator | Proximity-based store search with hours verification and service availability. |
| Open Box Sourcing | Identify discounted alternatives with transparent condition ratings. |
| Price Monitoring | Track product price changes and availability updates. |
| Retail Integration | Build shopping experiences integrated with Best Buy's product catalog and fulfillment. |
| Affiliate Commerce | Commission-based product recommendations with affiliate partner integration. |

## Integrations

| Name | Description |
|------|-------------|
| Postman | Pre-built Postman collection available for testing and exploring Best Buy APIs. |
| Impact Affiliate Network | Affiliate commission integration using Impact Partner ID for revenue attribution. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [Best Buy Products API](openapi/best-buy-products-api.yaml)
- [Best Buy Stores API](openapi/best-buy-stores-api.yaml)
- [Best Buy Recommendations API](openapi/best-buy-recommendations-api.yaml)

### JSON Schema

- [products-api-product-list-response-schema.json](json-schema/products-api-product-list-response-schema.json)
- [products-api-product-schema.json](json-schema/products-api-product-schema.json)
- [products-api-category-ref-schema.json](json-schema/products-api-category-ref-schema.json)
- [stores-api-store-list-response-schema.json](json-schema/stores-api-store-list-response-schema.json)
- [stores-api-store-schema.json](json-schema/stores-api-store-schema.json)
- [stores-api-store-service-schema.json](json-schema/stores-api-store-service-schema.json)
- [recommendations-api-recommendations-response-schema.json](json-schema/recommendations-api-recommendations-response-schema.json)
- [recommendations-api-recommended-product-schema.json](json-schema/recommendations-api-recommended-product-schema.json)

### JSON-LD

- [best-buy-products-api-context.jsonld](json-ld/best-buy-products-api-context.jsonld)
- [best-buy-stores-api-context.jsonld](json-ld/best-buy-stores-api-context.jsonld)
- [best-buy-recommendations-api-context.jsonld](json-ld/best-buy-recommendations-api-context.jsonld)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [Best Buy Products API](capabilities/shared/products-api.yaml) — 2 operations for product catalog access
- [Best Buy Stores API](capabilities/shared/stores-api.yaml) — 2 operations for store location lookup
- [Best Buy Recommendations API](capabilities/shared/recommendations-api.yaml) — 4 operations for behavioral recommendations

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Retail Discovery](capabilities/retail-discovery.yaml) | Products, Stores, Recommendations | 8 | Developer, Partner |

## Vocabulary

- [Best Buy Vocabulary](vocabulary/best-buy-vocabulary.yaml) — Unified taxonomy mapping 3 resources, 6 actions, 1 workflow, and 2 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [Best Buy Spectral Rules](rules/best-buy-spectral-rules.yml) — 28 rules across 9 categories enforcing Best Buy API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
