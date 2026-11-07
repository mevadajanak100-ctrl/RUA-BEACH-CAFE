# Rua Beach Cafe website

This is a static, single-file website. It uses vanilla HTML, CSS, and JavaScript; there is no build command or package installation.

## Run locally

Open `index.html` in a browser. For a local HTTP preview, use VS Code Live Server or another static file server so local images and external embeds behave as they will after deployment.

## Deploy to Vercel

Import this folder as a static project and use the project root as the deployment root. No build command or output directory is needed; Vercel serves `index.html` and the `images/` directory.

## Update the site

- Sign in at `/admin.html` to edit cafe details, opening hours, links, menu categories, dishes, and food photos without changing code. Changes are stored in the protected `site_content` Supabase row and the public site keeps its built-in fallback if the content API is unavailable.
- The menu data includes stable IDs and optional descriptions/images; only single-price dishes can be added to the client-side cart. Items with multiple or size-based prices remain call-to-confirm so the subtotal is not guessed.
- Replace gallery photos in `images/restaurant/` and `images/beach/`. Keep the image paths in `index.html` in sync, use descriptive alt text, and confirm you have permission to publish each photo.
- Replace the numbered pages in `images/food-menu/` and `images/bar-menu/` to update the original menu scans. Keep their `food-menu-01.webp` through `food-menu-11.webp` and `bar-menu-01.webp` through `bar-menu-11.webp` filenames unless you also update the menu scan list in `index.html`.
- Confirm menu prices, availability, dietary labels, and business details with the cafe before publishing changes.

`archive/` contains the pre-edit HTML backup and is excluded from deployment. Since unused photos were removed, this historical backup may reference images that are no longer present. `AUDIT.md` is project documentation and is also excluded from the public deployment.

The cart is browser-only: it saves to local storage when available, then provides a call link, copyable summary, and WhatsApp share link. It does not send orders or accept payment.

## Live booking setup

1. Create a Supabase project and run `supabase/schema.sql` in its SQL editor. For an existing project, run `supabase/content-migration.sql` before using the website editor, then run `supabase/security-hardening.sql` when applying the security changes.
2. Create a Resend account, verify the sender domain, and use the sender format in `.env.example`.
3. In Supabase Authentication, create the owner's email/password user. Add that user to `admin_users` with the SQL below:

   ```sql
   insert into public.admin_users (user_id, email, role)
   select id, email, 'owner'
   from auth.users
   where email = 'owner@example.com'
   on conflict (user_id) do update set role = 'owner', active = true;
   ```

4. Deploy on Vercel with every variable from `.env.example`. Keep `SUPABASE_SERVICE_ROLE_KEY` server-only.
5. Open the deployed HTTPS URL. Opening `index.html` directly uses preview-only local storage.
6. Test create, lookup, cancellation, owner email, guest email, and `/admin.html` before sharing the URL.

The API lives in `api/reservations.js`. It locks each date/time slot in PostgreSQL before confirming capacity, then sends owner and guest emails through Resend.

The protected owner dashboard lives in `admin.html` and `api/admin.js`. Supabase Auth sessions and the `admin_users` table enforce access; service-role credentials never reach browser code.

## Security hardening

- Set `BOOKING_ALLOWED_ORIGIN` to the deployed HTTPS origin. Use comma-separated origins in `BOOKING_ALLOWED_ORIGINS` only when preview domains are also required.
- Run `supabase/security-hardening.sql` after `supabase/schema.sql` when hardening an existing database. It closes direct public RPC access and adds database length/format constraints.
- Keep `SUPABASE_SERVICE_ROLE_KEY` and `RESEND_API_KEY` in Vercel server environment variables only. Never put them in browser code or `.env.example`.
- API rate limits are process-local best-effort protection. Add shared Redis/Upstash limiting before high-volume production traffic or multiple serverless regions.
- Test login throttling, booking throttling, lookup/cancellation throttling, origin rejection, direct RPC rejection, and security headers after deployment.
- Run `node tests/security-smoke.js` after security-related edits.
- Run `node tests/content-smoke.js` after content editor or validation edits.
- Test `/api/content`, admin content save/reset, public fallback content, menu edits, photo edits, and mobile layout after deployment.
