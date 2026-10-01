# Éclaté: setup guide

A premium 2.5D beauty and skincare theme for Shopify Online Store 2.0.

## 1. Install
1. **Online Store › Themes › Add theme › Upload zip file** and choose `eclate-beauty-theme.zip`.
2. Click **Customize** to edit. Every section, block, color and font can be changed there.
3. *(Developers)* Run `shopify theme dev --store your-store.myshopify.com` from this folder for live preview.

**External dependencies:** none. No JavaScript libraries are used. The fonts (Fraunces and DM Sans) load from Google Fonts;
untick *Theme settings › Typography › Use Éclaté fonts* to use the Shopify font library instead.

## 2. Menus (Online Store › Navigation)
- **Main menu**, for example: Shop · The Formula · Journal · Our World. Nested items become dropdowns. When a second level has
  its own children, the dropdown becomes a **mega menu**. Add a *Mega menu promo* block to the Header to show an image card in it.
- **Footer** menu: Support links (Shipping, Returns, Contact, FAQ).
- If no menu is selected, the header shows **Shop all** and **Collections** automatically.

## 3. Collections
Create your category collections (Skincare, Makeup, Body care, Fragrance, …), then pick them in:
- Home › **Beauty categories** (category cards)
- Collection template › **Product grid › Category tab** blocks (the "All / Skincare / Makeup / Body" tabs)

## 4. Beauty product metafields (optional, recommended)
**Settings › Custom data › Products › Add definition**

| Name | Namespace & key | Type | Used by |
|---|---|---|---|
| Subtitle | `custom.subtitle` | Single line text | Kicker above the title, card type label (e.g. "The Radiance Edit") |
| Highlights | `custom.highlights` | List of single line text | Benefit pills (Fragrance-free · Dermatologist tested…) |
| Ingredients | `custom.ingredients` | Multi-line or rich text | Product details › "Inside the bottle", Ingredients section |
| How to use | `custom.how_to_use` | Multi-line or rich text | Product details, How-to-use section |
| Results | `custom.results` | Multi-line or rich text | Product details › "Clinical results" |
| Skin type | `custom.skin_type` | List of single line text (Dry, Oily, Combination, Sensitive, Normal) | Skin types section highlights matching cards |
| Size | `custom.size` | Single line text | Product details › Size |
| Card badge | `custom.badge` | Single line text | Badge on product cards (Bestseller, New, Limited). A `badge:New` tag also works |
| Image badge | `custom.media_badge` | Single line text | Pill on the main product image (e.g. "15% active complex") |

Rows and blocks with no content are hidden automatically, so you don't need every field on every product.

## 5. Apps (free)
- **Shopify Search & Discovery**: collection filters (availability, price, product type, vendor, metafields) and
  complementary products for **Pair it with**.
- **A reviews app** (Judge.me, Okendo, Shopify Product Reviews, Yotpo…): stars appear on cards and the product page
  automatically (from the standard `reviews.rating` metafields). Add the app's block inside the **Reviews** section on
  the product template. The theme never shows invented reviews. Without an app, the Reviews section stays hidden from shoppers.
- **Wishlist**: a built-in browser wishlist is included (create a page with the `page.wishlist` template and select it in
  *Theme settings › Wishlist*). If you use a wishlist app, untick *Show wishlist hearts*.

## 6. Cart
*Theme settings › Cart*: drawer or page, the free-shipping threshold (the progress bar), promo code field, recommendations and order note.
Promo codes use Shopify's discount links, so codes from **Discounts** apply at checkout.

## 7. Sections included
**Home & content:** Hero (2.5D stage / split / full image), Featured products (grid or carousel), Beauty categories,
Benefits (panel / cards / pills), Story (brand or product story), Trust bar, Ingredients, Ritual steps / How to use,
Skin types, Testimonials, Blog posts, FAQ (with search markup), Newsletter, Promotional banner (cards / editorial),
Complete your routine (add-all bundle), Recently viewed, Custom Liquid.
**Optional extras (Add section in the editor):** Slideshow, Shop by concern, Featured product (spotlight with buy box),
Video (YouTube / Vimeo / upload, click-to-load), Scrolling text, Rich text, Countdown banner, "Find your ritual" skin quiz,
Shoppable gallery, Press & logos, Comparison table, Multirow, Multicolumn, Video reviews (TikTok / Reels style),
Before / after slider.
- **Skin quiz:** each answer has a *Filter parameter*, for example `filter.p.m.custom.skin_type=Dry` or
  `filter.v.price.lte=40`. Enable the matching filters in *Search & Discovery*, and the quiz opens the results collection already filtered.
- **Countdown:** the end date and time use the store's timezone. When it ends, the banner either hides or shows a message.
- **Video reviews / Before & after:** only use clips and photos from genuine customers that you have the rights to use.
**Product:** Product information (gallery, zoom, swatches, sticky add-to-bag), Product details (metafield accordions),
Reviews (app slot), Product recommendations.
**Collection:** Collection banner, Product grid (tabs, filters, sort, promo tile, load more), Collections list.

## 8. Known limitations
- Rating *breakdown bars* and individual review cards come from your reviews app's block. Shopify doesn't expose them to themes.
- The browser wishlist and recently viewed lists are stored on the shopper's device and don't sync across devices.
- Color swatches appear when option values have swatches set in Shopify (*Products › Variants › option value › swatch*).
- The **bundle discount** on "Complete your routine" must be created under *Discounts* (for example as an automatic discount); the section adds the products to the bag.
- `templates/index.sections-demo.json` is a QA page for previewing optional sections (`?view=sections-demo`). It's excluded from the release zip.

## 9. QA checklist (verified on a development store)
- [x] Online Store 2.0 architecture: sections everywhere, `{% schema %}` with settings, blocks and presets
- [x] JSON templates (index, product, collection, list-collections, cart, search, page, page.contact, page.wishlist, blog, article, 404, password, customers/*)
- [x] Section groups (header-group and footer-group) rendered from `layout/theme.liquid`
- [x] Theme Editor customization, with color schemes on every section
- [x] Dynamic products, collections and navigation (Shopify menus, with a fallback)
- [x] Product variants: pills and swatches, price, stock and image sync, unavailable states
- [x] Functional cart: add, quantity change, remove, notes, promo, free-shipping bar (AJAX Cart API)
- [x] Cart drawer, plus cart page with express checkout
- [x] Collection filtering (Search & Discovery), sorting, pagination with Load more
- [x] Search page and predictive search (products, collections, pages, articles, suggestions)
- [x] Product recommendations (related and complementary), loaded lazily
- [x] Responsive: 1440 / 1280 / 1024 / 768 / 390 / 375, with no horizontal overflow (tested)
- [x] Accessibility: semantic landmarks, labels, focus styles, keyboard dialogs, reduced-motion support, AA contrast
- [x] SEO: dynamic titles and meta, canonical URLs, Open Graph, Product / Breadcrumb / Article / FAQ / Organization / WebSite structured data
- [x] Performance: no frameworks, ~30 KB unminified JS, per-section CSS, responsive `image_url` / `image_tag`, lazy-loaded below the fold
- [x] 2.5D visual system: orbs, layered stage, glass cards, depth hover, floating motion, grain, CSS cosmetic art
- [x] Custom Liquid section
- [x] Shopify Theme Check: 0 offenses
