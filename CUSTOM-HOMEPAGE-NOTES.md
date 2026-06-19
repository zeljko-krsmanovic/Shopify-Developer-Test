# Custom Homepage — Build Notes

A custom, fully Theme‑Editor‑editable homepage built from six self‑contained sections.
All content is exposed through section/block schema settings — no hard‑coded copy
(schema `default`s are placeholders only).

## Files

| Area | File | Editable via |
| --- | --- | --- |
| Shared styles | [assets/custom-homepage.css](assets/custom-homepage.css) | Linked from every section; dynamic values come through inline CSS variables |
| Hero | [sections/custom-homepage-hero.liquid](sections/custom-homepage-hero.liquid) | Section settings |
| Benefits | [sections/custom-homepage-benefits.liquid](sections/custom-homepage-benefits.liquid) | Section settings + `benefit` blocks |
| Featured Products | [sections/custom-homepage-featured-products.liquid](sections/custom-homepage-featured-products.liquid) | Section settings (`product_list`) |
| Collections | [sections/custom-homepage-collections.liquid](sections/custom-homepage-collections.liquid) | Section settings (`collection_list`) |
| Reviews | [sections/custom-homepage-reviews.liquid](sections/custom-homepage-reviews.liquid) | Section settings + `review` blocks |
| Footer | [sections/custom-homepage-footer.liquid](sections/custom-homepage-footer.liquid) | Section settings + `link_group` / `social` blocks |
| Homepage wiring | [templates/index.json](templates/index.json) | Section order + default content |

The homepage template renders, in order: **Hero → Benefits → Featured Products → Collections → Reviews**.

## How each requirement is met

- **Hero** — heading (`text`), subheading (`richtext`), primary + optional secondary CTA
  (`text` + `url`), hero image (`image_picker`) with an alt‑text override field, image
  position (left/right), background image **or** colour (`color_background`), and text colour.
  Every field is wrapped in `{% if ... != blank %}` so nothing renders empty.
- **Benefits** — 2–4 reorderable `benefit` blocks, each with icon/image, title, text, and an
  optional link. Column count, gap and alignment are configurable. Ships with 3 preset blocks.
- **Featured Products** — `product_list` picker (drag to reorder, up to 12). Each card shows
  image, title, price (with sale handling) and a button that either links to the product or
  **adds the first available variant to the cart** (real `/cart/add` form, works without JS).
  Optional "View all" button + configurable products‑per‑row.
- **Collections** — `collection_list` picker. Each card shows the collection image (falls back
  to the first product's image), title, a description excerpt, and a "Shop" button. Layout
  toggle: responsive **grid** or a CSS‑only **swipe carousel** (no JS).
- **Reviews** — reorderable `review` blocks: reviewer name, review text (`richtext`), 1–5 star
  rating (`range`, rendered as ★), optional reviewer photo, and an optional linked product
  (`product` picker). Ships with 3 preset reviews.
- **Footer** — about logo + text, one or more `link_group` blocks (each picks a navigation
  menu via `link_list`), contact info (address / phone / email), `social` blocks (icon image
  + link), and an auto‑generating copyright line.
- **Global / per‑section settings** — every section has: show/hide toggle, page‑width vs
  full‑width, background colour, text colour, and top/bottom padding. Images carry alt text
  and use `image_url` + responsive `srcset`/`sizes`.

## Responsiveness

- Breakpoint `749px` matches the theme's mobile breakpoint.
- Desktop: multi‑column grids (configurable). Tablet (`≤990px`): products/collections drop to
  2‑up. Mobile (`≤749px`): hero stacks (content first), benefits/reviews/collections go single
  column, products stay 2‑up, and buttons become full‑width and tap‑friendly.
- All images use `max-width:100%` / `object-fit: cover`; no horizontal overflow.

## Theme Editor — how to edit each section

Open **Online Store → Themes → Customize** with the **Home page** template selected.

1. **Hero** — click the Hero section: edit heading, subheading, primary/secondary button
   label + link, swap the hero image, change image position, background and text colour.
2. **Benefits** — expand the section, click a benefit block to edit icon/title/text/link.
   Use the drag handle to reorder, the "+" to add (max 4), the trash icon to remove.
3. **Featured Products** — open the **Products** picker to select/reorder products; set
   products‑per‑row; choose the button action (link vs add‑to‑cart); set the "View all" link.
4. **Collections** — open the **Collections** picker to choose/reorder collections; toggle
   grid vs carousel; set cards‑per‑row.
5. **Reviews** — add/edit/reorder/remove review blocks; change name, text, star rating, photo,
   and optional linked product.
6. **Footer** *(see placement note below)* — edit about text/logo, link‑group headings and
   their menus, contact details, social blocks, and copyright.
7. **Visual settings** — change any section's background colour or top/bottom padding and watch
   the live preview update. Use the **Show section** toggle to hide/show a section (hidden
   sections appear dimmed in the editor and disappear on the live store).

## Footer placement (important)

This theme already renders a site‑wide footer through `sections/footer-group.json`
(included in [layout/theme.liquid](layout/theme.liquid#L130-L132)). To avoid a double footer,
`custom-homepage-footer` is **not** added to the homepage by default. To use it, either:

- **Replace the site footer (recommended):** in the Theme Editor footer area, remove the
  existing footer and add **Custom Footer**; or edit `sections/footer-group.json` to reference
  `custom-homepage-footer`.
- **Add to a single template:** add it as the last section on any template via "Add section".

The footer's link groups use the `link_list` setting, so create the menus under
**Online Store → Navigation** (the blocks default to the `footer` menu handle).

## Assumptions & limitations

- Base theme: **Shopify Horizon** (theme‑blocks architecture). Sections use plain‑English
  schema labels (not the theme's `t:` translation keys) so they are fully self‑contained.
- Featured Products "Add to cart" adds the **first available variant**; products with required
  variant selection are better linked to the product page (the default button action).
- The Collections carousel is CSS scroll‑snap (swipe / trackpad) — no arrow buttons, to avoid
  shipping unverified JavaScript. Switch to "Grid" for a static multi‑column layout.
- `templates/index.json` was updated to use these sections; the previous demo sections (`hero`,
  `product-list`) are still available in the theme and can be re‑added from "Add section".

## Submission checklist (to capture)

- [ ] Preview link / collaborator access (or theme export / GitHub repo).
- [ ] Screenshots or short video of the finished homepage — **desktop and mobile**.
- [ ] Theme Editor clips for each area: Hero edit, Benefits add/reorder/remove, Featured
      Products selection + View‑all, Collections selection, Reviews add/edit, Footer link
      groups + contact, and one visual change (background colour / padding).
- [ ] This notes file.

## Validation done

- All six `{% schema %}` blocks and `templates/index.json` parse as valid JSON.
- Empty‑state placeholders for Products/Collections render **only in the Theme Editor**, never
  to live shoppers.
