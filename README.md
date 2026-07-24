# Premier Countertops — Marketing Site (Hero Redesign)

A modernized landing page for [premiertops.com](https://www.premiertops.com/), built
around a **scroll-pinned 3D hero** that scrubs a countertop being installed
(template scan → slab lowered with sink cutout → sink/faucet → full kitchen reveal),
followed by materials, process, services, gallery, testimonials, a quote form, and
footer. Warm Southern-craftsmanship voice; CTA: *Request a free quote.*

**Status: pitch demo** (structured to grow into a production launch). This is a
polished, deployable page to show Premier Countertops — not yet the live site.

## How it was built

The design was created in **Claude Design** (`Premier Countertops.dc.html`, kept in
[`design/`](design/) for provenance). That file is a Design Component that depends on
Claude's proprietary `support.js` runtime, so it can't be served standalone as-is.

`index.html` is a faithful, self-contained port:

- **All markup and the entire three.js (r128) scene are preserved verbatim** from the
  design — maximum fidelity, no drift.
- The proprietary `support.js` runtime is replaced by a ~60-line vanilla-JS
  compatibility shim (inlined in `index.html`) that implements only the directives the
  page uses: `ref`, `onClick`/`onSubmit`, `sc-if`, `style-hover`, `image-slot`
  placeholders, and `state`/`setState`.
- Hero "Tweaks" are baked to the approved defaults: **Calacatta White / Sage / Warm**.

No build step, no dependencies. It's a single static HTML file (three.js loads from a
CDN; Google Fonts from Google).

## Run locally

```bash
cd premier-site
python3 -m http.server 8123
# open http://localhost:8123
```

## Known scope (pitch demo)

- **Quote form is a visual mockup** — it shows a "Thank you" state on submit but does
  not send anything yet.
- **Gallery images are labeled placeholders** — swap in real project photos for launch.

## Growth path (launch later)

- Wire the quote form to a real endpoint (reuse the Resend setup in the sibling
  `premier-intake` project's `lib/email.ts`; optionally persist leads to Supabase).
- Replace gallery placeholders with real photography.
- SEO/meta polish, sitemap, redirects from old premiertops.com URLs, then DNS cutover
  (only with Premier's go-ahead).
- Optionally re-expose the material/daylight switcher as an on-page control so visitors
  can preview stone options.
