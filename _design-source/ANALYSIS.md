# Éclaté: design analysis & architecture (Stages 1–2)

Source: Canva "2.5D beauty Shopify theme" (three Canva Code pages).
Screens of the live design: `screens/live-*.jpg`. The copy and colors extracted from each page are in `home|product|collection.json`.

## 0. Inconsistencies found in the Canva files (and how they're resolved)

| Issue | Resolution |
|---|---|
| Three brand names: Lumière (home), Éclaté (product), Aurelia (collection) | One brand. Uses `shop.name` / logo, with the demo copy written for "Éclaté" |
| Three body fonts: DM Sans (home, collection) and Work Sans (product) | **Fraunces** (display serif) + **DM Sans** (body) everywhere |
| Three palettes (cocoa/lilac, ink/terracotta, wine/sage) | One palette with **color schemes** that keep each page's accent surfaces |
| Currencies: $ (home) and ₹ (product, collection) | Always `money` filters (store currency) |
| Monkey photo on a product card; 2 ingredient cards and 2 promo cards have no image | Image settings fall back to 2.5D CSS "cosmetic object" art |
| Routine steps numbered 01 / 03 / 02 | Numbers come from block order |
| Newsletter button wraps over 3 lines ("Join / the / list") | Pill button set to `white-space: nowrap` |
| Collection "Recently viewed" has one oversized card | Even rail of product cards |
| Clay CTA #bd6251 with white text = 4.18:1 (fails AA) | Clay deepened to **#a8503f** (5.41:1); clay labels use the same color |
| Gold stars #c79455 = 2.49:1 | **#a8763b** (3.64:1, passes the non-text 3:1 minimum) |

## 1. Visual system

**Palette**
| Token | Hex | Use |
|---|---|---|
| Cocoa (ink) | #3e2b29 | text, primary pill buttons, dark scheme |
| Cream | #fbf5ed | page background |
| Pearl | #fffaf5 | cards |
| Blush | #efb7b2 / #f6ddd5 | orbs, reassurance panel, newsletter button |
| Lilac | #d9c9e8 / #e6d8e8 | orbs, benefit & routine panels |
| Sand | #eadbd0 | ingredients section |
| Clay | #a8503f | add-to-bag, kicker labels |
| Plum | #5b2637 | announcement, newsletter band |
| Sage | #617062 | editorial callout |
| Muted text | #7a5f5c | secondary copy (5.36:1 on cream) |

**Typography:** Fraunces 400–600 for display headings (tight −0.02em, line-height 0.95–1.1).
DM Sans 400–700 for body. Kickers are 11–12px, uppercase, letter-spacing 0.24em, bold.
Scale: display clamp(2.8–4.6rem), H2 clamp(2–3rem), H3 1.25–1.5rem, body 16px.

**Shape:** cards 28px, panels 32px, images 22px, pills 999px, the hero frame an organic `44% 44% 35% 35%`.

**Shadows (soft, diffuse):** `0 22px 45px rgba(80,53,51,.14)` float, and `0 24px 44px rgba(77,49,47,.16)` lift on hover.
Product page "lift" = an offset blush shadow `10px 12px 0 rgba(233,140,117,.2)` plus a diffuse shadow.
Collection "stage" = a neumorphic gradient with inset light/dark edges.

**2.5D effects**
1. **Orbs:** large blurred circles in blush and lilac bleeding off the edges.
2. **Layered hero stage:** a rotated gradient organic blob, a rotated glass outline, a photo with an organic radius, a floating frosted card and a tilted pill badge.
3. **Floating:** slow 5–6s drift (translateY ±10px, rotate ±3°).
4. **Depth cards:** a hover lift of −8px with a tiny rotate and a bigger shadow; the product image rises on hover.
5. **Glass:** `backdrop-filter: blur(14px)`, translucent white and an inset highlight.
6. **Grain:** an optional 5px dot noise overlay on the product gallery.
7. **Reveal:** rise-in on view (0.7s) when animations are on.
All of it is disabled under `prefers-reduced-motion`.

**Spacing:** sections pad 96px (desktop) / 56px (mobile), content max width 1280px, gutters 32px / 20px, card gaps 20–24px.

## 2. Page & section map

**Home:** Announcement → Header → Hero (layered stage + stats) → Featured products ("Best-loved essentials") →
Benefits panel → Brand story → Trust bar → Product carousel ("Bestsellers, on repeat") →
Ingredients → Ritual steps → Testimonials → Journal (blog posts) → FAQ → Newsletter → Footer.

**Product:** Breadcrumb → Main product (gallery + info + benefit pills + reassurance panel) → Details accordion →
Ingredients (lift cards) → Complete your routine (products + "add the routine") → Reviews → FAQ →
"Pair it with" (complementary recommendations) → Recently viewed → mobile sticky add-to-bag.

**Collection:** Breadcrumb → Collection hero (faded image, floating framed product, orb, pill) → Category tabs + sort →
Filters sidebar ("Refine") + grid (with an editorial promo tile inside the grid) → Load more →
Recently viewed → Promo cards ("A little more to love") → Newsletter band.

**Added beyond the design (spec):** beauty categories, promotional banner, how to use, skin types, product story,
cart page, search, blog/article/page/contact/404/password/account templates, cart drawer with recommendations
and promo code, custom Liquid.

## 3. Component map → files
| Component | File |
|---|---|
| Product card (styles: `soft` home card, `stage` collection card) | snippets/product-card.liquid |
| Price / badge / rating / icon / button / responsive image | snippets/price, badge, rating, icon, button, responsive-image |
| Product form + variant picker | snippets/product-form, variant-picker |
| Cart line | snippets/cart-item |
| Breadcrumb / pagination | snippets/breadcrumb, pagination |
| 2.5D primitives (orbs, cosmetic objects) | snippets/decor.liquid, snippets/cosmetic-art.liquid |
| Section heading | snippets/section-heading.liquid |

## 4. Shopify data
- Menus: `main-menu`, `footer`, plus extra footer menus
- Product metafields (all optional): `custom.subtitle` (kicker), `custom.highlights` (list, used as benefit pills),
  `custom.ingredients`, `custom.how_to_use`, `custom.results`, `custom.skin_type` (list), `custom.size`,
  `custom.badge` (card badge, e.g. "Bestseller")
- Reviews: the standard `reviews.rating` / `reviews.rating_count` (written by Judge.me, Okendo, Shopify Product Reviews…)
- Search & Discovery: filters and complementary products

## 5. Responsive strategy
- 1440 / 1280: full layouts, 4-column grids
- 1024: the hero stage shrinks; grids go to 3 columns; the filter sidebar becomes a drawer
- 768: 2 columns; the hero stacks with the art first; the product gallery is full width with the info below
- 390 / 375: 2-column product grid (setting allows 1); rails swipe; mobile sticky add-to-bag; a full-screen menu sheet;
  orbs are smaller and kept inside the viewport (no horizontal overflow)
