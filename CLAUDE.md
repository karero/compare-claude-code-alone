# Fernwood Technical Translation — website

Static Astro site for Cloudflare Pages. Live address: https://compare-cc-alone.pages.dev
Edited after launch by Jo Fernwood with an AI coding assistant. Keep changes small and plain.

## Commands
- `npm install` — once, after cloning
- `npm run dev` — local preview at http://localhost:4321
- `npm run build` — builds the site into `dist/` (this is what Cloudflare Pages publishes)

Cloudflare Pages settings: build command `npm run build`, output directory `dist`.
Do not deploy from here; publishing is handled separately.

## Where things are
- `src/site.ts` — business name, email, phone, footer notice, navigation. Change contact details here only.
- `src/pages/` — one file per page: `index.astro` (home), `services.astro`, `about.astro`, `contact.astro`, `404.astro`.
- `src/layouts/Base.astro` — page shell: `<head>`, header, footer. Every page uses it.
- `src/components/Header.astro`, `Footer.astro`
- `src/styles/global.css` — all styling; colours are CSS variables at the top.
- `public/` — files copied as-is (favicon, robots.txt).

## Rules that must hold
- Every page footer says: "A fictional business, built for a comparison. Not a real service." (set in `src/site.ts`, shown by `Footer.astro`).
- Only these contact details: email jo@example.com, phone +1 555 0142. No street address.
- Do not invent customers, testimonials, quotes, client names, figures, awards or certifications.
- One language (English). No analytics, no tracking scripts, no server code, no contact form — contact is by email link.
- Pages: home, services, about, contact. No blog.
