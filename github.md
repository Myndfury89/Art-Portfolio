# Art-Portfolio — sync log

Human-readable changelog for site syncs to `main` (Myndfury89/Art-Portfolio).

## Last sync

- **When:** 2026-08-29T14:28:09-0700
- **Commit:** `c1effa3f47840fbc5a12fb83b8f4ae42c4c988af` (merge of PR #4, branch `fix/concept-lightbox-componentdidupdate`)
- **Fix — empty Concept Team lightbox on `work.html`:** clicking any Concept Team tile (Black Resume / God Game / Survival Idol / System Royale) opened the lightbox with the correct title but **no images**.
  - **Root cause:** `componentDidUpdate(prevProps, prevState)` read a second `prevState` arg, but the `support.js` framework invokes `logic.componentDidUpdate(prevProps)` with no `prevState` (support.js:1013). `prevState` was always `undefined`, so the first line threw `TypeError: Cannot read properties of undefined (reading 'activeProject')` before `_renderLightbox()` (the only code that populates the grid) could run. The framework's try/catch swallowed it, so it surfaced only as a repeating console error.
  - **Fix:** track the previously-rendered project on the instance (`this._lastProject`) instead of relying on the `prevState` arg the framework never provides. One method changed in `work.html`; `support.js` untouched.
- **Verified in production** (`myndfurycreative.com/work`, real Chrome via CDP): all four lightboxes populate — Black Resume 18/18, God Game 11/11, Survival Idol 5/5, System Royale 10/10 = **44/44 images loaded**, no broken paths, no image 404s, **no console errors**; open/close/reopen and project-switching all work. Non-regression confirmed: work-page anchors scroll, the Black Resume case-study modal opens/closes, and mobile (390px) lightbox loads — all clean.

## Sync history

- **2026-08-28T16:17:34-0700** — `292db4cce4713ecd9b2cb7b3d93c5859ac5c7547`
  - **Copy edits (3):** small wording changes only — no markup, assets, or SEO tags touched.
    - **Home / Black Resume:** direction paragraph now ends at "…and built a human-led AI production process around them." (trailing clause about the artists' turnarounds and finished pages becoming the models' reference removed).
    - **Home / AI Lab teaser:** now reads "I structured a testing framework, checked against multiple characters." (was "A structured testing framework — one direction, checked against multiple characters.").
    - **AI Lab / "A shared visual language":** paragraph now reads "Using my skillset in webtoon/cinematography, I created a visual language that could be applied and repeated." (replaces the "standardized terms / vocabulary I already used directing artists" wording).
  - Applied as targeted edits to the two live pages; the staged export also carried unrelated changes (dropped `<title>`/`<meta description>` on both pages, an `<img>`→`<image-slot>` swap on AI Lab) which were **not** taken. No `.dc.html` links or `myndfury@gmail.com` introduced.

- **2026-08-27T08:29:09-0700** — `90eb73f36396330c52e1c108a3ab7ef7a8ec4b0c`
  - **Work:** page made fluid/mobile-friendly; new Black Resume banner header; hero image swap; Black Resume logo repositioned.
  - **AI Lab:** new "From Intent to Image" case study (reference characters, prompt-testing table, failure case, shot-language cards) moved to the top of the page under a new header image; supporting stills added under `ai-eval/`.
  - **Home:** VoyceMe & FableVerse copy and system cards simplified; AI Lab teaser added.
  - **Contact:** page replaced with a working inquiry form.
  - Personal email (`myndfury@gmail.com`) removed from all deployed pages — Home, Work, AI Lab, Contact, and About; the About bio/footer links now route to the `/contact` inquiry form. (Only the deploy-excluded legacy `Home-standalone-src.dc.html` still contains it.)
  - Stripped the vestigial `image-slot.js` script (404'd on deploy) from `index.html` and `ai-lab.html`; converted AI Lab's `<image-slot>` camera-diagram placeholder to a static `<img src="media/assets/ai-lab-camera-diagram.webp">` so the diagram renders. All 233 referenced files now deploy (0 excluded).
  - **Verification (2026-08-27T09:22:28-0700):** full-site broken-link sweep across all five pages — 234/234 local assets and 5/5 internal routes return 200 live; external links resolve (the lone `fonts.googleapis.com` 404 is the preconnect origin hint, not a fetched resource); no `mailto:` remains anywhere. Site is clean.
  - **Contact form wired to Formspree (2026-08-27T20:06, commit `18b51de6de24beeadae3f3c5ed4dcb05d0e95681`):** replaced the no-op submit with an AJAX `fetch` to `https://formspree.io/f/mqpkkzvd` (no page reload) — client-side validation (name/email/message), a hidden `_gotcha` honeypot, disabled/loading button ("Send message →" → "Sending…"), and inline `aria-live` success/error states; entered values preserved on failure. No `mailto`, no secrets.
  - Regenerated `.vercelignore` (deploy allow-list) so the newly-referenced root `uploads/` and `assets/` files ship — the pages now point at those paths, which were being excluded and 404'd on the first deploy. 232/233 referenced files deploy; the lone exclusion is the vestigial `image-slot.js` script tag (unused editor tooling, still re-introduced in this export).

- **2026-08-24T07:51:08-0700** — `51f9cb2a7cf469e249bc54b52acec8f3e5aade8a`
  - Removed the stale `<script src="./image-slot.js">` tag from `index.html` — the script was excluded from deploy (unused editor tooling, replaced by static `<img>`), so it 404'd in production on every homepage load. No other reference to it existed.
  - Reconciled the `## Screen map` Files column with each page's actual assets: **Home** now lists `assets/`, `media/home/`, `uploads/`; **Work** lists `media/`, `media/assets/`, `media/uploads/`; **About**, **AI Lab**, and **Contact** verified accurate.

- **2026-08-23T21:29:03-0700** — `c9c7b5304e34795e3412952c7e2febc8ff9c5ca4`
  - Fixed broken images on the live homepage: the deploy allow-list (`.vercelignore`) was excluding root `assets/` and `uploads/` files the rebuilt homepage references, so they 404'd in production despite existing in the repo.
  - Now deploys the referenced `assets/` files — hero stills, `matt-portrait.jpg`, the 18 `client-*.png` logos, and the `ref-frame-*`/`after-frame-*` "Direction in / Result out" frames — plus `uploads/Zokio5367-b4b9cf1d.png` (Zokio #5367 sheet), `uploads/BR2.png` (character design sheet), and `uploads/Avon.png`.
  - Hardened `scratch/genignore.mjs` (local tooling): `assets/` now default-denies with per-file re-includes like `uploads/`, and the scanner also catches template-literal asset paths (`` `assets/ref-frame-${n+1}.png` ``).
- **2026-08-23T21:10:19-0700** — `b158b04c3d46112c7661c41790c279e5489ab499`
  - Homepage rebuilt below the portrait as a single image-led scroll: **01 Thrash / Craft**, **02 Black Resume / Direction**, **03 VoyceMe & FableVerse / Leadership**, **04 AI Lab / Innovation**, **05 More Worlds / Range**, **06 Philosophy**, **07 CTA**.
  - **No modals** — one "Explore the case study" link per section.
  - Added **Zokio #5367** and **Kain8** character sheets to Black Resume.
  - All four pages made **fluid for mobile**.
  - **21 homepage images compressed to WebP** under `media/home/`.
- **2026-08-21T20:46:18-0700** — `45d188ce5bca7361c1c1505653e8f134aeaa5e8d`
  - Added case study **"07 — McLane Highlanders"** (senior night poster series for McLane High School girls basketball).
  - New modal covering **high energy / explosiveness / one locked template**, plus a **four-poster Series grid with 200% hover zoom**.
  - Four posters compressed to **WebP at 850px** (`media/uploads/mclane-cherish.webp`, `mclane-latique.webp`, `mclane-tina.webp`, `mclane-steph.webp`).

## Screen map

| Screen | Route | Files |
| --- | --- | --- |
| Home | index.html | index.html, assets/, media/home/, uploads/ |
| Work | work.html | work.html, media/, media/assets/, media/uploads/ |
| About | about.html | about.html, media/assets/matt-portrait.webp |
| AI Lab | ai-lab.html | ai-lab.html, media/assets/ai-lab-camera-diagram.webp, media/uploads/ |
| Contact | contact.html | contact.html, media/uploads/ |
