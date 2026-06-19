# Custom Shopify Homepage — Project Deliverable

Preview link: https://zeljko-testprocessing.myshopify.com/?_ab=0&_bt=eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaEpJaWg2Wld4cWEyOHRkR1Z6ZEhCeWIyTmxjM05wYm1jdWJYbHphRzl3YVdaNUxtTnZiUVk2QmtWVSIsImV4cCI6IjIwMjYtMDYtMTlUMDI6MjE6MjMuNTA2WiIsInB1ciI6InBlcm1hbmVudF9wYXNzd29yZF9ieXBhc3MifX0%3D--6eaa717e776ee5813805d21e8f85b9f20721fa3b&_fd=0&_sc=1&key=527697dfa32ba5baf8fecf6dad28c579f5e7be0a5406420af48fb58debd0d624&preview_theme_id=190529634669
<br>
Password: rtibre


A custom, **fully merchant-editable** homepage built for Shopify (Horizon theme). The homepage
is composed of six purpose-built sections — **Hero, Benefits, Featured Products, Collections,
Reviews, and Footer** — each configurable end-to-end from the **Shopify Theme Editor** with no
code changes required.

> **Status:** ✅ Complete and validated. All sections load in the Theme Editor and render
> responsively on desktop, tablet, and mobile.

---

## 1. What was delivered

| # | Section | Highlights | Editable in Theme Editor |
|---|---------|-----------|--------------------------|
| 1 | **Hero** | Heading, description, primary + secondary buttons, hero image, image left/right, background image or colour, text colour | ✔ |
| 2 | **Benefits** | 2–4 reorderable benefit items, each with icon, title, text, optional link | ✔ |
| 3 | **Featured Products** | Merchant-picked products, image · title · price (sale-aware), product link **or** add-to-cart, “View all” button | ✔ |
| 4 | **Collections** | Merchant-picked collections, image · title · description · “Shop” button, grid **or** swipe carousel | ✔ |
| 5 | **Reviews** | Add/edit/reorder testimonials: name, text, 1–5 star rating, photo, optional linked product | ✔ |
| 6 | **Footer** | About + logo, link menus, contact details, social links, auto copyright | ✔ |

**Everything visible on the page is editable** — no hard-coded text or images. Each section also
includes a show/hide toggle, width, colour, and spacing controls.

---

## 2. Live preview & how to view

1. In the Shopify admin, go to **Online Store → Themes**.
2. On this theme, click **Customize**.
3. Make sure the **Home page** template is selected (top dropdown).
4. The six sections appear in order in the left-hand panel.

> A preview/collaborator link or theme export accompanies this delivery (see the project handover
> message). The screenshots below show the final result.

---

## 3. Video

> Replace the placeholders below with the exported images before sending to the client.

https://drive.google.com/file/d/15elEsdxQFOwYPv8fY2NK36aqXmmg8pH3/view?usp=sharing


---

## 4. How to edit each section (for the client)

Open **Customize → Home page**, then click any section in the left panel.

| Section | What you can change |
|---------|--------------------|
| **Hero** | Heading, description, button labels + links, hero image (and alt text), image position (left/right), background colour/image, text colour, padding |
| **Benefits** | Click a benefit to edit its icon, title, text, and link. Drag to reorder, **＋** to add (max 4), 🗑 to remove. Set columns and alignment |
| **Featured Products** | Open the **Products** picker to choose/reorder products. Set products-per-row, button behaviour (link vs add-to-cart), and the “View all” link |
| **Collections** | Open the **Collections** picker to choose/reorder collections. Toggle Grid vs Carousel and cards-per-row |
| **Reviews** | Add/edit/reorder review blocks: reviewer name, text, star rating, photo, optional linked product |
| **Footer** | Edit about text/logo, link-group menus, contact info, social links, and copyright *(see Footer note in section 6)* |
| **Any section** | **Show section** toggle, page/full width, background & text colour, top/bottom padding |

Changes save instantly and appear in the live preview.

---

## 5. Responsive design

- **Desktop:** multi-column layouts (column counts are configurable per section).
- **Tablet (≤ 990px):** product and collection grids drop to 2 columns.
- **Mobile (≤ 749px):** sections stack into a single column (hero shows content first), product
  grid stays 2-up, and buttons become full-width and tap-friendly.
- All images scale fluidly with responsive `srcset`; no horizontal overflow at any width.

---

## 6. Technical notes

**Files added**

```
assets/
  custom-homepage.css                       # Shared, responsive styles for all sections
sections/
  custom-homepage-hero.liquid               # Hero
  custom-homepage-benefits.liquid           # Benefits (blocks)
  custom-homepage-featured-products.liquid  # Featured Products (product_list)
  custom-homepage-collections.liquid        # Collections (collection_list)
  custom-homepage-reviews.liquid            # Reviews (blocks)
  custom-homepage-footer.liquid             # Footer (blocks)
templates/
  index.json                                # Homepage — wires the 5 sections in order
CUSTOM-HOMEPAGE-NOTES.md                     # Detailed developer notes
README.md                                    # This file
```

**Built to Shopify best practices**

- Section + block schemas using native picker types: `product_list`, `collection_list`,
  `image_picker`, `richtext`, `url`, `range`, `color`/`color_background`, `link_list`, `product`.
- Clean, commented Liquid; content output only when set (no empty tags).
- One shared, cacheable stylesheet; dynamic values passed via CSS variables.
- Responsive images via `image_url` + `srcset`/`sizes`; alt text on every image.
- Add-to-cart uses Shopify’s standard cart route and works without JavaScript.

**Footer placement (important)**

This theme already shows a site-wide footer (via `footer-group.json`). To avoid two footers, the
custom **Custom Footer** section is delivered as a standalone, ready-to-use section but is **not**
auto-added to the homepage. To make it live, either add it from **Add section**, or swap it into
the theme’s footer area. Full steps are in [CUSTOM-HOMEPAGE-NOTES.md](CUSTOM-HOMEPAGE-NOTES.md).

---

## 7. Assumptions & limitations

- Base theme: **Shopify Horizon**. Sections are self-contained and use plain-English labels.
- Featured Products’ add-to-cart adds the **first available variant**; products needing variant
  selection are best shown with the “Link to product page” button (the default).
- The Collections carousel is a CSS swipe carousel (no arrow buttons), keeping the build
  dependency-free and fast.
- `templates/index.json` was set up to use these sections; the theme’s original demo sections
  remain available and can be re-added anytime.

---

## 8. Handover checklist

- [x] Six custom sections built and editable in the Theme Editor
- [x] Homepage assembled (Hero → Benefits → Featured Products → Collections → Reviews)
- [x] Responsive across desktop / tablet / mobile
- [x] Schemas and template validated
- [ ] Preview/collaborator link or theme export shared with client
- [ ] Final screenshots added to `docs/screenshots/`
- [ ] Client walkthrough of editing each section

---

*Prepared by Tempest Digital. Questions or change requests welcome.*
