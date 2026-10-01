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
