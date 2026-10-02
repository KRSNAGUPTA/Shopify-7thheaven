# 7th Heaven — Shopify Liquid MVP

Interview MVP for the **pincode → cake → date/slot → message → checkout** flow, built as a **Shopify Online Store 2.0 Liquid theme** (not headless Next.js).

## Why Liquid (not Next.js)

The JD lists Liquid as a core requirement and Next.js as a preference. This repo ships the same end-to-end flow in a theme so you can demo:

- Theme sections / templates merchants can edit
- Cart line item properties on Shopify orders
- Hosted Shopify checkout (Bogus Gateway for test orders)

A headless Next.js + Storefront API version is a natural Phase 2 if the interviewer cares about React.

## Architecture

```
Customer (theme)
  → Pincode check (localStorage + static map)
  → Product form (variant + line item properties)
  → Cart AJAX API → cart drawer
  → /checkout (Shopify hosted)
```

**Fulfilment attributes on each cart line:**

| Key | Example |
|---|---|
| Message on cake | Happy Birthday! |
| Delivery date | 2026-10-04 |
| Delivery slot | Morning (11 AM - 1 PM) |
| Fulfilment store | 7th Heaven Andheri |

## Scope (MVP)

**Built**

1. Home (hero, categories, featured collection, trust strip, franchise teaser)
2. Collection grid
3. Product page: weight/type variants, message, date, slots, sticky ATC
4. Pincode → Andheri / Thane (static map in header JS)
5. Cart drawer + cart page → Shopify checkout
6. Store locator (`/pages/stores` with `page.stores` template)
7. Franchise enquiry (`/pages/franchise` contact form)

**Phase 2 (skipped)**

Reviews, WhatsApp, search, accounts, multi-currency, full menu, metaobject-driven serviceability, multi-location inventory sync.

## Setup

1. Shopify Partner account + development store
2. Collections: `cakes`, `cupcakes`, `desserts`
3. Products with weight + egg/eggless variants
4. Optional product metafields: `custom.serves`, `custom.prep_hours`, `custom.eggless_available`
5. Create pages **Stores** and **Franchise**, assign templates **stores** and **franchise**
6. Enable Bogus Gateway for test checkout
7. Preview:

```bash
shopify theme dev
```

### Sample serviceable pincodes

| Pincode | Store |
|---|---|
| 400053, 400058, 400061, 400069, 400093 | Andheri |
| 400601, 400602, 400603, 400604, 400606 | Thane |

In production this map would move to a **metaobject** or Locations API — explained here so the MVP stays a static JSON-equivalent in theme JS.

## Demo flow

1. Enter pincode `400053` in the header
2. Open Cakes → pick a product
3. Choose variant, message, date, slot → Add to cart
4. Cart drawer shows attributes → Checkout
5. Place a Bogus Gateway order; confirm line properties in admin

## Production notes (talking points)

- **Pincode / store mapping:** metaobjects or Admin Locations + inventory per location
- **Shopify Plus / multi-store:** inventory by location, delivery profiles, or Hydrogen for a custom storefront
- **Same product page in Liquid:** already implemented here (`sections/product-template.liquid`)

## License

MIT (based on Shopify Skeleton Theme).
