# Éclaté: Shopify OS 2.0 beauty theme

A premium soft-2.5D beauty and skincare theme, converted from the Canva design "2.5D beauty Shopify theme".

- **Merchant setup, metafields, limitations and the QA checklist:** [GETTING-STARTED.md](GETTING-STARTED.md)
- **Design analysis and architecture (Stages 1–2):** [`_design-source/ANALYSIS.md`](_design-source/ANALYSIS.md)

## Structure
```
assets/      theme.css · theme.js · component-product.css · section-*.css (loaded only by their section)
config/      settings_schema.json (color schemes, typography, layout, 2.5D, cards, cart…) · settings_data.json
layout/      theme.liquid · password.liquid
locales/     en.default.json
sections/    header-group.json · footer-group.json · 48 sections (main-*, hero, featured-products, story, …)
snippets/    product-card · price · badge · rating · icon · button · responsive-image · product-form ·
             variant-picker · cart-item · cart-summary · pagination · breadcrumb · cosmetic-art · decor · …
templates/   JSON templates + customers/* + gift_card.liquid
```

## Develop
```bash
shopify theme dev --store <store>.myshopify.com
shopify theme check
```
Push only the files you changed, so edits made in the theme editor aren't overwritten:
```bash
shopify theme push --store <store>.myshopify.com --theme <id> --only sections/hero.liquid
```

## Release zip
Zip `assets config layout locales sections snippets templates` with forward-slash paths. Leave out
`templates/index.sections-demo.json` (QA only).

## Keeping in step with the store builder

The store builder's copy (`store-builder/themes/eclate/src`) is the live version. It has these, applied there:
- the hardening passes
- the theme editor in nine languages (`t:` keys, `locales/*.schema.json`)
- the add-ons kits in `scripts/theme-addons`, including the product-information blocks: Emoji benefits, Urgency text, Clickable discount, Shipping checkpoints and Quantity selector

This repo was synced from that copy on 2026-10-15.

After changing files here:
1. Commit, then import the theme: `node scripts/import-theme.mjs eclate ../eclate-beauty-theme`
2. Key and translate any new editor labels:
   - `node scripts/theme-schema-i18n.mjs eclate`
   - `railway run node scripts/i18n-translate.mjs schema`
3. Copy `themes/eclate/src` back here, so the two stay identical.

Never import an older checkout of this repo: it would undo the fixes made in the app.
