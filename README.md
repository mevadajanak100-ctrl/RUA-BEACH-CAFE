# Rua Beach Cafe website

This is a static, single-file website. It uses vanilla HTML, CSS, and JavaScript; there is no build command or package installation.

## Run locally

Open `index.html` in a browser. For a local HTTP preview, use VS Code Live Server or another static file server so local images and external embeds behave as they will after deployment.

## Deploy to Vercel

Import this folder as a static project and use the project root as the deployment root. No build command or output directory is needed; Vercel serves `index.html` and the `images/` directory.

## Update the site

- Edit page content, styles, menu categories, and menu items in `index.html`. The menu data includes stable generated IDs and optional descriptions/images; only single-price dishes can be added to the client-side cart. Items with multiple or size-based prices remain call-to-confirm so the subtotal is not guessed.
- Replace gallery photos in `images/restaurant/` and `images/beach/`. Keep the image paths in `index.html` in sync, use descriptive alt text, and confirm you have permission to publish each photo.
- Replace the numbered pages in `images/food-menu/` and `images/bar-menu/` to update the original menu scans. Keep their `food-menu-01.webp` through `food-menu-11.webp` and `bar-menu-01.webp` through `bar-menu-11.webp` filenames unless you also update the menu scan list in `index.html`.
- Confirm menu prices, availability, dietary labels, and business details with the cafe before publishing changes.

`archive/` contains the pre-edit HTML backup and is excluded from deployment. Since unused photos were removed, this historical backup may reference images that are no longer present. `AUDIT.md` is project documentation and is also excluded from the public deployment.

The cart is browser-only: it saves to local storage when available, then provides a call link, copyable summary, and WhatsApp share link. It does not send orders or accept payment.
