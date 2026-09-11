# SSHD2368 Motion Media — Course Website

PolyU CPCE / HKCC · Semester One 2026/2027  
Subject Leader & Lecturer: CHAN, Long-fung Lazarus

Static site ready for **GitHub Pages**. Lecture HTML (weeks 1–10) and the tutorial guide are **self-contained** (images embedded as base64). Week 11 is an in-class test — no lecture deck is published.

## Password gate

The whole site (home + slides) asks for a password before content is shown.

- **Password:** `20262368`
- Unlock lasts for the browser tab session (`sessionStorage`).
- This is **client-side only** (suitable for casual course access, not strong security).

To change the password, edit `PASSWORD_HASH` in [`auth.js`](auth.js):

```bash
python3 -c "import hashlib; print(hashlib.sha256(b'YOUR_PASSWORD').hexdigest())"
```

## Publish with script (Mac)

```bash
cd Github/SSHD2368
./publish.sh
```

Pushes to [2026-1-SSHD2368-MOTION-MEDIA-Group-A01-](https://github.com/Lazaruschan/2026-1-SSHD2368-MOTION-MEDIA-Group-A01-). Sign in if Git prompts you. Then enable Pages once: **Settings → Pages → main / (root)**.

## Publish on GitHub Pages (simplest)

1. Create a new empty GitHub repository (e.g. `SSHD2368-Motion-Media`).
2. Upload **the contents of this folder** as the repo root (not the parent `Github/` folder).
   - Include: `index.html`, `auth.js`, `.nojekyll`, `assets/`, `slides/`, `README.md`
   - Do **not** upload `node_modules/`
3. In the repo: **Settings → Pages → Build and deployment**
   - Source: **Deploy from a branch**
   - Branch: `main` (or `master`), folder: **/ (root)**
4. Wait a minute, then open `https://<user>.github.io/<repo>/`

`.nojekyll` is included so GitHub Pages serves files as-is (no Jekyll processing).

### Via git (optional)

```bash
cd Github/SSHD2368
git init
git add index.html auth.js .nojekyll .gitignore README.md assets slides
# optional tooling (not required for Pages):
# git add export-slides.sh embed-slide-assets.py package.json package-lock.json
git commit -m "Publish SSHD2368 Motion Media course site"
git branch -M main
git remote add origin https://github.com/<USER>/SSHD2368-Motion-Media.git
git push -u origin main
```

Then enable Pages as above.

## Open locally

Open [`index.html`](index.html) in a browser, or:

```bash
cd Github/SSHD2368
python3 -m http.server 8080
```

Visit `http://localhost:8080`.

- Lecture decks: [`slides/week-01.html`](slides/week-01.html) … [`slides/week-10.html`](slides/week-10.html)
- Studio guide: [`slides/tutorials.html`](slides/tutorials.html)
- Briefs: [`assets/briefs/`](assets/briefs/)

## Rebuild slides from Marp sources (maintainers)

Requires Node (nvm) and source files under `Notes/Motion_Media/Motion_Media/`.

```bash
cd Github/SSHD2368
npm install
./export-slides.sh
```

This regenerates weeks 1–10 + tutorials, embeds local images/diagrams into the HTML, and removes any temporary `slides/images` / `slides/diagrams` folders.

## Site structure (publish)

```
SSHD2368/
  index.html
  auth.js                 Password gate (required)
  .nojekyll
  .gitignore
  README.md
  assets/briefs/          Assessment PDFs
  slides/
    week-01.html … week-10.html   (self-contained)
    tutorials.html                (self-contained)
```

The reusable blank template for other courses is [`../template.html`](../template.html).
