# Bundle Banner (Shopify Section) + Intelligems PDP Test

This README documents:
1) the **Bundle Banner** Shopify section implementation (Task 1), and  
2) the **Intelligems** test setup to compare the existing PDP hero vs. the new banner (Task 2).

---

## 1) Overview

### What we built (Task 1)
A reusable **Shopify section** named **“Bundle Banner”** that renders a promotional banner with:

- Heading + optional accent text
- Subheading
- CTA button (link to collection or product)
- Optional full-banner link (collection/product)
- Background image (desktop + mobile) with gradient fallback
- Product image (desktop + mobile)
- Responsive layout:
  - **Mobile (<1024px):** product image on top, text below
  - **Desktop (≥1024px):** background banner with text overlay (product image hidden per current CSS)

**Notes on implementation:**
- Mobile-first, vanilla CSS only (no Tailwind).
- Uses `section.id` to scope CSS: `.bundle-banner--{{ section.id }}` to avoid style collisions.
- Uses Shopify image filters: `img_url` for sizing (`2000x`, `800x`, `800x`, `600x`).
- Includes Google Font loading (`Libre Baskerville`) inside the section.

---

## 2) Folder Structure

Expected theme structure for this change:
/sections
bundle-banner.liquid
/templates
product.control.json
product.bundle-banner.json

### Key files
- `sections/bundle-banner.liquid`
  - The section code provided in this task.
- `templates/product.control.json`
  - Control PDP template (existing hero only).
- `templates/product.bundle-banner.json`
  - Variant PDP template (existing hero + Bundle Banner section added).

> Template filenames may vary depending on the theme (e.g. `main-product`, `product`, etc.).  
> The important part is having **two PDP templates**: one for Control and one for Variation.

---

## 3) Setup Steps (Shopify)

### A) Add the section to the theme
1. Create file: `sections/bundle-banner.liquid`
2. Paste the full Bundle Banner code.
3. Save.

### B) Create Control vs Variant PDP templates
1. Shopify Admin → **Online Store → Themes → Customize**
2. Open any product page (PDP).
3. In the template selector:
   - Duplicate the current product template.
4. Rename templates:
   - **Control:** keep the existing template (e.g. `new-template`)
   - **Variant:** new template (e.g. `product.template`)
5. On the **Variant** template:
   - Add section **“Bundle Banner”** in the desired position on the PDP.
6. Save.

### C) Configure section settings
In the theme editor for the Variant template, adjust:
- Heading text + accent
- Subheading
- CTA label + CTA destination (collection/product)
- Optional banner link (makes the entire banner clickable)
- Desktop/mobile background images
- Desktop/mobile product images
- Button colors and typography sizing

---

## 4) Intelligems Experiment Setup

### Goal
Create an A/B test on the dev store:

- **Control:** existing PDP hero section
- **Variation:** PDP template that includes the Bundle Banner (Task 1)
- **Target:** product pages only (not homepage/collections)
- **Primary metric:** add-to-cart rate (measured via ATC click event)
- **Secondary metric:** revenue metric (Revenue per Visitor in our UI)
- **Traffic split:** 50/50

### Test Type
- Intelligems: **Content → Template**

### Test ID
- Intelligems ID:
159f3c23-2711-42a9-84de-aa3d3fea8cef
(aa3d3fea8cef)

---

## 5) URL Targeting Rules


### Option B (Specific products only)
If limiting to specific PDPs:

- `urlPath` contains `/products/bundle-product`  
  **OR**
- `urlPath` contains `/products/bundle-product-copia`

---

## 6) Metrics Setup

### Primary Metric (Add-to-cart rate)
Configured as an Intelligems **Custom Metric → Click Interaction**:

- **Event name:** `Add to Cart Click (PDP)`
- **Selector used:**
  ```css
  button[data-testid="standalone-add-to-cart"]

  
