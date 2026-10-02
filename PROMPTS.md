# AI Prompt Log — Mistvale Tea Co.

## Prompt 1
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Serene panoramic morning view of lush misty Darjeeling tea hills at dawn, rolling green terraced tea plantations shrouded in gentle morning fog, warm golden morning light, soft atmospheric depth, calm earthy aesthetic, high resolution photography, natural light, premium organic tea brand header background
- Outcome: accepted
- Why: Produced an authentic, warm, and serene hero banner with rolling misty tea terraces matching the brand personality perfectly.

## Prompt 2
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Square product studio photography of premium Assam Breakfast Black Tea. An earthy craft paper tea pouch bag sitting on a warm natural linen and light wood surface, next to a small white ceramic dish holding rich, malty dark granular Assam CTC black tea leaves. Soft warm morning sunlight, natural shadows, minimalist luxury packaging, clean cream background.
- Outcome: accepted
- Why: Rendered high-end artisan packaging and clear granular CTC tea leaves with consistent studio lighting on wood/linen.

## Prompt 3
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Square product studio photography of premium Darjeeling First Flush tea. An earthy craft paper tea pouch bag sitting on a warm natural linen and light wood surface, next to a small white ceramic dish holding delicate whole spring harvest tea leaves with greenish-golden tips. Soft warm morning sunlight, natural shadows, minimalist luxury packaging, clean cream background.
- Outcome: accepted
- Why: Clean whole spring harvest tea leaves with golden tips matching the delicate floral product description.

## Prompt 4
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Square product studio photography of premium Kashmiri Kahwa tea. An earthy craft paper tea pouch bag sitting on a warm natural linen and light wood surface, next to a small white ceramic dish holding whole green tea leaves blended with visible red saffron strands, whole green cardamom pods, cinnamon bark pieces, and almond flakes. Soft warm morning sunlight, natural shadows, minimalist luxury packaging, clean cream background.
- Outcome: accepted
- Why: Accurately captured green tea leaves with distinct red saffron strands, whole cardamom, and almond flakes.

## Prompt 5
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Square product studio photography of premium Masala Chai Blend tea. An earthy craft paper tea pouch bag sitting on a warm natural linen and light wood surface, next to a small white ceramic dish holding rich dark CTC black tea leaves blended with aromatic spices including dried ginger pieces, green cardamom pods, whole cloves, and crushed black peppercorns. Soft warm morning sunlight, natural shadows, minimalist luxury packaging, clean cream background.
- Outcome: accepted
- Why: Rich, aromatic whole chai spices clearly visible beside the artisan pouch bag with warm natural lighting.

## Prompt 6
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Square product studio photography of premium Nilgiri Green Tea. An earthy craft paper tea pouch bag sitting on a warm natural linen and light wood surface, next to a small white ceramic dish holding whole emerald green, smooth, grassy twisted green tea leaves. Soft warm morning sunlight, natural shadows, minimalist luxury packaging, clean cream background.
- Outcome: accepted
- Why: Showcases vibrant green twisted whole tea leaves with identical background and angle to the rest of the collection.

## Prompt 7
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Square product studio photography of premium Chamomile & Tulsi herbal tea. An earthy craft paper tea pouch bag sitting on a warm natural linen and light wood surface, next to a small white ceramic dish holding dried yellow chamomile flower blossoms and aromatic green holy basil tulsi leaves. Soft warm morning sunlight, natural shadows, minimalist luxury packaging, clean cream background.
- Outcome: accepted
- Why: Clear herbal ingredients (dried chamomile flowers and green tulsi leaves) on a ceramic dish matching the pouch.

## Prompt 8
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Square product studio photography of premium Hibiscus Rose Infusion tea. An earthy craft paper tea pouch bag sitting on a warm natural linen and light wood surface, next to a small white ceramic dish holding dried deep crimson red hibiscus calyces and delicate dried pink rose petals. Soft warm morning sunlight, natural shadows, minimalist luxury packaging, clean cream background.
- Outcome: accepted
- Why: Vibrant crimson hibiscus petals and pink rose petals that clearly convey a tart, floral infusion.

## Prompt 9
- Tool: Gemini 3.7 (Imagen 3)
- Type: image
- Prompt:
  > Square product studio photography of premium Tea Lover's Sampler Gift Box. An open handcrafted artisan wooden tea gift box with compartments showcasing six small elegant tea tins and a rolled parchment brewing guide, set on a warm natural linen and light wood surface. Soft warm morning sunlight, natural shadows, luxury gift packaging, clean cream background.
- Outcome: accepted
- Why: Beautiful open wooden gift box showcasing 6 miniature tins and a parchment brewing guide, perfectly matching product 108 description.

## Prompt 10
- Tool: Gemini 3.7 (Claude / Antigravity Assistant)
- Type: code
- Prompt:
  > Implement the complete vanilla JavaScript business logic for the Mistvale online store in index.html following rules R1 through R8: calculate all prices from PRODUCTS, enforce quantity caps (max 5 or stock), handle WELCOME10 coupon (10% off eligible items excluding category Gifts, max ₹150 discount, subtotal >= 399), calculate ₹49 shipping or free over ₹499 post-discount, ensure sold out items are strictly sorted last, unify search/filters/sort with race-condition prevention, and handle API.checkPincode promise errors.
- Outcome: modified
- Why: The initial logic forgot to exclude the "Gifts" category from coupon discount calculations and used an unstable array sorting comparator. I added `calculateEligibleSubtotal()` and a multi-tier comparator `compareProducts()`.

## Prompt 11
- Tool: Gemini 3.7 (Claude / Antigravity Assistant)
- Type: code
- Prompt:
  > Generate the full CSS design system tokens and HTML markup for index.html strictly using BRAND.md rules: custom properties for colors (#1f3d2b, #4f7942, #f6f1e7, #ebe2cf, #d9962b, #1b1b1b, #b3261e), Google Fonts Fraunces & Inter with display=swap, sentence case headings, 8px spacing, 2-column mobile grid, inline SVGs with no icon fonts, zero external libraries, structured JSON-LD schemas (OnlineStore, ItemList, FAQPage), and required page sections in exact specified order.
- Outcome: modified
- Why: Removed an unwanted `transition: all` rule and added WCAG AA focus rings (`:focus-visible`) and `prefers-reduced-motion` media queries.
