# Art-Portfolio — sync log

Human-readable changelog for site syncs to `main` (Myndfury89/Art-Portfolio).

## Last sync

- **When:** 2026-08-23T21:29:03-0700
- **Commit:** `__PENDING__`
- Fixed broken images on the live homepage: the deploy allow-list (`.vercelignore`) was excluding root `assets/` and `uploads/` files the rebuilt homepage references, so they 404'd in production despite existing in the repo.
- Now deploys the referenced `assets/` files — hero stills, `matt-portrait.jpg`, the 18 `client-*.png` logos, and the `ref-frame-*`/`after-frame-*` "Direction in / Result out" frames — plus `uploads/Zokio5367-b4b9cf1d.png` (Zokio #5367 sheet), `uploads/BR2.png` (character design sheet), and `uploads/Avon.png`.
- Hardened `scratch/genignore.mjs` (local tooling): `assets/` now default-denies with per-file re-includes like `uploads/`, and the scanner also catches template-literal asset paths (`` `assets/ref-frame-${n+1}.png` ``).

## Sync history

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
| Home | index.html | index.html, media/home/ |
| Work | work.html | work.html, media/uploads/mclane-*.webp |
| About | about.html | about.html |
| AI Lab | ai-lab.html | ai-lab.html |
| Contact | contact.html | contact.html |
