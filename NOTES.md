# Mistvale Tea Co. — Developer Assessment Notes

## 1. What I Changed

### Bugs & Business Rules
- **Rule R1 (Pricing from Data):** Refactored cart calculation functions (`calculateSubtotal`, `renderCart`, `addToCart`) to strictly use `PRODUCTS` array data and unit price numbers, eliminating DOM scraping (`parseInt(innerText)`).
- **Rule R2 (Quantity & Stock Limits):** Implemented strict quantity caps enforcing `1 <= qty <= Math.min(5, product.stock)` on both direct grid adds, Quick View, and stepper inputs. Handled edge cases where items reached maximum allowed capacity.
- **Rule R3 (Coupon WELCOME10):** Re-engineered the coupon engine to be case-insensitive, require a subtotal >= ₹399, exclude the "Gifts" category (`product.category === 'Gifts'`) from discount calculations, and cap discounts at ₹150 maximum. Fixed the compounding discount bug where repeated clicks added multiple discounts.
- **Rule R4 (Free Shipping & Thresholds):** Configured shipping to ₹49 and free on orders >= ₹499 calculated on the net amount *after* discount. Implemented a dynamic progress bar showing the exact remaining amount needed.
- **Rule R5 (Indian Currency Formatting & Rounding):** Applied `Math.round()` only to the final order total and formatted every monetary amount using `₹` and Indian digit grouping (`en-IN`, e.g., ₹1,299).
- **Rule R6 (Sold-Out Product Placement):** Guaranteed that sold-out items (stock = 0) can never be added to cart and strictly sort to the very end across all sort orders (Price Low to High, High to Low, Name A-Z, Featured).
- **Rule R7 (Unified Search, Category Filter, and Sort):** Unified state handling so searching, category selection, and sorting cooperate seamlessly without overwriting each other. Implemented a request ID counter and debounce to prevent race conditions from asynchronous `API.search` responses.
- **Rule R8 (Delivery Pincode Check):** Added error handling (`.catch()`) for `API.checkPincode` promise rejections and client-side format validation to eliminate UI freezes on "Checking...".
- **Cart Array & Event Listener Leaks:** Fixed `localStorage` initialization to prevent null pointer exceptions (`JSON.parse(...) || []`), corrected string vs number comparisons (`===`), fixed `array.splice(index, 1)` bug that previously deleted all subsequent items, and eliminated duplicate click listener bindings on render.
- **Checkout Form Contract:** Preserved `<form id="checkout-form">` with `action="https://mistvale.example/cart/checkout"` and populated `items` JSON and `coupon` hidden fields upon checkout trigger.

### Design & Brand System
- **Brand Identity & Color Tokens:** Extracted all CSS custom properties from `BRAND.md` (`--color-tea-green`, `--color-leaf`, `--color-cream`, `--color-parchment`, `--color-saffron`, `--color-ink`, `--color-error`) and removed all unapproved colors, neon highlights, and gradients.
- **Typography & Font Hierarchy:** Replaced Comic Sans/Pacifico/Oswald with Google Fonts pair (**Fraunces** for headings and **Inter** for body text) using a single `<link>` with `display=swap`. Applied fluid typography using CSS `clamp()`.
- **Spacing & Structure:** Built an 8px spacing system, responsive container (`max-width: 1200px`), and 2-column mobile grid expanding to 4-columns on desktop.
- **Micro-Interactions & States:** Added 200ms transitions on specific properties, accessible `:focus-visible` saffron focus rings, hover lifts on product cards, and full `@media (prefers-reduced-motion: reduce)` support.

### UX & Usability
- **Removed Annoying Popups & False Claims:** Removed the 2-second disruptive newsletter popup in favor of a clean inline section. Stripped fake badges (e.g., "As Seen on Shark Tank India" and unverified 10,000+ review claims).
- **Enhanced Shopping Drawer & Quick View:** Created an accessible slide-out cart drawer with free shipping progress bar, inline coupon manager, quantity steppers, and a Quick View modal with pack size selection.
- **Toast Notifications:** Added subtle, non-intrusive feedback toast when items are added or updated in the cart.

### Technical & SEO
- Removed external jQuery and FontAwesome libraries; implemented lightweight native vanilla JS and inline SVGs.
- Added comprehensive Open Graph, Twitter card, canonical tags, and structured JSON-LD schemas (`OnlineStore`, `ItemList`/`Product`, and `FAQPage`).

---

## 2. What the AI Got Wrong

1. **Initial Filter/Sort Implementation:** The initial AI-generated sort function attempted to mutate the array with an incomplete boolean comparator (`a.price > b.price`), which produced unstable sorting in Chrome, and completely ignored the business rule requiring sold-out products to always sort last. I caught this and wrote a custom multi-tier comparator `compareProducts()` that checks `stock === 0` first.
2. **Coupon Calculation on Gift Items:** When asked to calculate the discount, the AI initially applied 10% on the entire cart subtotal including the Tea Lover's Sampler Gift Box. I caught this against Rule R3 and added a dedicated `calculateEligibleSubtotal()` function filtering out `p.category === 'Gifts'`.
3. **Pincode Error Handling:** The AI initially called `API.checkPincode(pin)` assuming all errors would be caught by an `if (res.error)` check inside `.then()`, failing to realize that `API.checkPincode` rejects with `new Error('INVALID_PINCODE')`. This left the widget permanently stuck on "Checking...". I added a proper `.catch()` handler with user-friendly error copy.
4. **CSS Animation:** The AI initially attempted to add `transition: all 0.3s ease` to all elements, violating the brand rule prohibiting `transition: all`. I refactored the styles to explicitly target `transform`, `background-color`, `border-color`, `color`, and `box-shadow`.

---

## 3. Images

- **Hero Banner (`images/hero-banner.jpg`):** Generated using Gemini / Imagen 3 with a prompt focusing on a serene morning view of rolling misty Darjeeling tea terraces in natural sunlight. Resized and compressed to 1440x810 at 82% quality (236 KB, within the 250 KB limit).
- **Product Images (`images/p101.png` to `images/p108.png`):** Generated using Gemini / Imagen 3 with consistent framing, studio lighting, craft packaging, and loose leaf botanicals on linen and wood surfaces. Resized to 700x700 square format and web-compressed (57 KB to 95 KB each, well below the 150 KB limit).
- **Logo (`images/logo.svg` & `images/logo.png`):** Crafted a minimalist vector SVG logo featuring Darjeeling mountain peaks, a tea leaf mark, and serif typography matching the brand palette.

---

## 4. How I Tested It

- **Automated Browser End-to-End Testing:** Executed full functional workflows via browser subagent covering search autocomplete, category filtering, low-to-high and high-to-low sorting, out-of-stock sorting priority, pincode check with valid (`734001`) and invalid inputs, Quick View modal, cart additions, coupon calculation (`WELCOME10`), gift box discount exclusion, and quantity capping at 5 units.
- **Console Inspection:** Verified zero uncaught exceptions, zero console warnings, and clean network requests.
- **Keyboard Navigation & Accessibility:** Tested `Tab` / `Shift+Tab` focus flow across all interactive controls, verified `:focus-visible` focus rings, and tested `Escape` key listeners for modals and drawers.
- **Screen Resizing:** Verified fluid responsiveness across 360px mobile viewport, 768px tablet, and 1200px desktop screens without any horizontal overflow.

---

## 5. Questions for the Team

1. **Free Shipping Announcement vs Code Default:** The original announcement banner mentioned ₹499 while the previous buggy JavaScript had `sub > 599`. We standardized the business logic and UI to ₹499 based on Rule R4 and the brand announcement.
2. **Gift Packaging Option:** Should gift messages entered by customers during checkout be passed as an additional property in the `items` JSON payload or as an extra header field?

---

## 6. Time Spent

- **Total Time:** ~3.5 hours
  - Analysis & bug auditing: 30 minutes
  - Core logic, business rules & API integration: 45 minutes
  - Brand styling, CSS tokens & responsive layout: 45 minutes
  - Image generation, optimization & logo creation: 40 minutes
  - End-to-end testing, accessibility & documentation: 50 minutes

---

## 7. Extra Features I Added

1. **Wishlist Drawer:** Shoppers can save favorite teas with local persistence, view their wishlist in a slide-out drawer, and move items directly into the cart.
2. **URL State Synchronization:** Category filters, search terms, and sort selections automatically sync with URL query parameters (e.g. `?cat=Black&sort=low`), allowing customers to share exact filtered product views.
3. **Pack Size Selector in Quick View:** Added interactive 100g standard and 250g family pack size selector.
4. **Interactive Free-Shipping Progress Bar:** Visual progress bar in the cart drawer calculating the remaining amount to reach free shipping.
5. **Toast Feedback System:** Non-intrusive notification feedback for cart and wishlist actions.

---

## 8. With More Time I Would…

1. Add localized bilingual support (e.g. Hindi / English toggle).
2. Implement automated brew timer guides directly in the Quick View modal for each tea variety (temperature & steep countdown).
3. Add multi-pack subscription discount options (e.g., monthly Darjeeling first flush delivery).
