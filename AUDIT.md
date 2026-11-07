# Rua Beach Cafe Website Audit

Baseline: `index.html` and the existing files in `images/`, inspected before implementation. The pre-edit page is preserved at `archive/index.original.html` and excluded from deployment.

## High priority

| Area | Finding | Change |
|---|---|---|
| Accuracy / conversion | Ratings, costs, menu details, and business claims need a source and can change between public listings. | Attribute the current Google Maps and District ratings separately, show District's indicative cost for two with attribution, and link to the live source listings. Keep booking, phone, and exact Google Maps directions prominent. |
| Menu / ordering accuracy | Menu photos contain dish names and prices, but availability and current pricing may change; diet labels need confirmation for ambiguous items. There is no ordering backend. | Build collapsible category navigation and search/filter controls from the local menu scans, transcribe printed dish names/prices, mark uncertain dietary classifications for staff confirmation, show all 11 food and 11 bar scan pages in an accessible lightbox, and provide a localStorage-backed client-side cart that ends in call/copy/WhatsApp handoff. Do not imply order submission or payment. |
| Restaurant claims | Public listing details change, and review wording/photos lack verified permission. | Use District's current cuisine labels in structured data, include verified hours and Maps coordinates, and replace unsupported experience-price claims with attributed listing facts. Link to original reviews instead of copying review text or platform photos. Keep “Since 2024” unchanged and flag it for manager verification. |
| Images / rights | Photo filenames and earlier captions did not consistently match the visible content; local photo rights and menu correspondence are not verified. | Rename the six displayed restaurant images to reflect their visible content, keep descriptive captions and the accessible lightbox, and use the three supplied local beach/cafe photographs with descriptive alt text. Link to District and Google Maps for source photos; do not republish platform photos without permission. |
| Booking and location | Business name/address/rating need consistent verified details; location directions should use the current Google Maps listing. | Normalize the name and contact text; add the complete address, correct District URL, click-to-call, Google Maps place link, hours, and matching Restaurant JSON-LD. |
| Deployment / SEO | Canonical production domain is unknown; current JSON-LD misses postal code and geo; local discovery metadata can be improved. | Add social metadata and a clearly marked canonical-link placeholder comment (do not emit a false canonical URL); add Restaurant JSON-LD from verified facts only and the verified cuisine list. |
| Security / external services | The site has no user-generated input/backend; external District and Maps pages must be isolated when opened in new tabs. | Keep listing and map links on fixed URLs with `rel="noopener noreferrer"`; do not claim the site accepts orders or payments. |

## Medium priority

| Area | Finding | Change |
|---|---|---|
| Mobile navigation | The mobile menu has no Escape handling and needs predictable close behavior. | Ensure expanded state stays synchronized and the menu closes on link selection, Escape, outside click, or transition to desktop. |
| External listing data | Third-party ratings, costs, hours, and menus can change; a dedicated Zomato listing could not be verified. | Attribute dated Google Maps and District ratings, cost, and cuisine labels, link to the original sources, and show no Zomato rating until its listing is verified. |
| Gallery accessibility | Native dialog behavior is not enough to guarantee the requested navigation/focus experience in all supported browsers. | Keep previous/next, close, Escape/arrow key support, touch swipe, captions, focus trap/return, and mobile zoom-friendly sizing for the cafe photos shown on the page. |
| Mobile menu visibility | The tall menu browser could not reach the 12% visibility threshold used by the reveal animation on a phone, leaving its search, filters, and category accordions transparent. | Trigger reveals when at least 1% of an element is visible so tall mobile sections can appear as guests scroll to them. |
| Keyboard and motion | Interactive images, reduced-motion behavior, focus feedback, and keyboard access require explicit checks. | Keep visible focus indicators, support reduced motion, enforce lightbox focus trapping/return, and use keyboard-operable gallery controls. |
| Performance / Core Web Vitals | The remaining local image collection totals approximately 7.41 MiB, primarily because all 22 menu scans are retained for reading; only the lead image should load eagerly, while other assets need dimensions to reduce CLS. | Prioritize the hero image, set dimensions, lazy-load/decode noncritical images, keep interactions lightweight, and provide graceful broken-image styling. Do not claim measured LCP/CLS/INP without a deployed URL and lab run. |
| Design system | The previous palette and some component styles are inconsistent with the requested navy/cyan direction. | Use named CSS tokens for background, surfaces, accents, text, success/error, borders, and shadows; retain a restrained coastal identity and readable contrast. |
| Contact content | The alternate phone number and social links have not been verified/provided. | Keep the supplied primary number; do not publish the alternate or fabricate social links; list both confirmation needs in the handoff. |

## Low priority

| Area | Finding | Change |
|---|---|---|
| Code quality | The single HTML file contains unused styles/handlers and inline presentation styles. | Remove confirmed dead code, move inline presentation to named CSS classes, and keep the implementation dependency-free and in one HTML file. |
| Polish | The page can provide useful return navigation and motion preferences. | Retain and verify scroll progress, active-section styling, back-to-top, subtle reveal effects, and reduced-motion support. |
| Responsive quality | A visual design can appear responsive but still overflow at narrow or very wide viewports. | Check 320, 360, 390, 768, 1024, 1440, and 1920 CSS-pixel viewports for horizontal overflow and touch-target sizing. |

## Verification limits and manager follow-up

- Google Maps showed 4.2 from 865 reviews; District showed 4.2 from 1,081 ratings, 85 written reviews, and an indicative ₹2,300 cost for two when checked October 4, 2026. These figures are dynamic and must not be treated as permanent.
- District listed North Indian, Italian, and Indo-Chinese when checked. Zomato did not yield a verifiable dedicated Rua Beach Cafe listing; no Zomato rating or review is displayed.
- Confirm that all printed menu pages, transcribed prices, dish availability, and dietary labels are current before launch; the webpage links to District and phone for verification.
- Confirm the “Since 2024” claim before launch; it is retained unchanged pending confirmation.
- Confirm publishing rights for the six local gallery photos and other identifiable cafe photos; confirm whether each food photo matches a currently offered item.
- Confirm permission to publish the three new local beach/cafe photographs and that the images represent Rua Beach Cafe.
- Confirm whether +91 7738174846 is a valid alternate phone number before adding it.
- Guest review text and platform photos are linked rather than reproduced; obtain permission before adding review excerpts or platform images.
- Confirm any alcohol, parking, kid-friendly, pure-vegetarian, or live-music claims before publishing; none are asserted here.
- Obtain an authorized restaurant-owned/licensed replacement image set if any current local photos cannot be cleared. Images displayed in Google Maps, Zomato, or District are not automatically licensed for republication.
- Replace the canonical URL placeholder with the live HTTPS domain and run Lighthouse against the deployed URL before calling Core Web Vitals production-verified.
