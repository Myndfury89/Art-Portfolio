# Matt Johnson — Portfolio

Static site. No build step, no dependencies.

## Pages
- `index.html` — redirects to the homepage
- `Home.dc.html` — homepage
- `Work.dc.html` — case studies
- `AI Lab.dc.html` — AI process work
- `Contact.dc.html` — contact + testimonials
- `support.js` — runtime required by all pages
- `assets/`, `assets-opt/`, `uploads/` — images and media

## Deploying

**Netlify (drag and drop)**
1. Go to app.netlify.com/drop
2. Drag this whole folder in
3. Done — you get a live URL immediately

**Netlify via GitHub**
1. Push this folder to a GitHub repository
2. In Netlify: Add new site → Import an existing project → pick the repo
3. Build command: leave blank. Publish directory: `/`

**GitHub Pages**
1. Push to a repo
2. Settings → Pages → Deploy from branch → `main` / root

## Notes
- Must be served over HTTP, not opened from the filesystem.
- `assets-opt/` holds compressed copies used by the standalone export.
