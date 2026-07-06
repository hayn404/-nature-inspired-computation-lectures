# Nature Inspired Computation — Lecture Slides

This repository holds the [Slidev](https://sli.dev) slide decks for the **Nature Inspired Computation (DSAI 403)** course. Each lecture lives in its own folder and can be run, edited, and exported independently.

## Repository structure

```
nature-inspired-computation-lectures/
├── lecture-01-introduction/
│   ├── slides.md        # the lecture content (Slidev markdown)
│   ├── style.css        # global style tweaks for this lecture
│   └── assets/          # images used in the slides
├── package.json          # Slidev CLI + convenience scripts
├── .gitignore
└── README.md
```

Future lectures will be added the same way: `lecture-02-.../slides.md`, `lecture-03-.../slides.md`, etc.

---

## Prerequisites

- **Node.js** version 20.12.0 or newer. Check yours with:
  ```bash
  node -v
  ```
  If you don't have Node.js, install it from [nodejs.org](https://nodejs.org).

You do **not** need to install Slidev globally — it's listed as a project dependency and run through `npx`/npm scripts, so everyone who clones this repo gets the same version.

---

## 1. Clone the repository

```bash
git clone https://github.com/<your-username>/nature-inspired-computation-lectures.git
cd nature-inspired-computation-lectures
```

## 2. Install dependencies

```bash
npm install
```

This downloads Slidev and its theme into `node_modules/` (this folder is git-ignored, so it won't be committed).

## 3. Run a lecture locally

Each lecture has its own npm script. For Lecture 1:

```bash
npm run lecture-01
```

This starts a local dev server and opens the deck in your browser, typically at:

- **Slide show:** http://localhost:3030/
- **Presenter mode:** http://localhost:3030/presenter/
- **Slide overview:** http://localhost:3030/overview/

The page live-reloads whenever you edit `slides.md`.

If you'd rather run Slidev directly instead of using the npm script (e.g. for a new lecture folder that doesn't have a script yet), you can always do:

```bash
npx slidev lecture-02-whatever/slides.md --open
```

### Useful keyboard shortcuts while presenting

| Key | Action |
|---|---|
| `→` / `Space` | Next click / slide |
| `←` | Previous click / slide |
| `f` | Toggle fullscreen |
| `o` | Toggle slide overview |
| `d` | Toggle dark mode |

---

## 4. Exporting slides

Slidev can export any deck to **PDF**, **PPTX**, or **PNG images**. The first time you export, it will ask permission to install `playwright-chromium` (a headless browser used to render the slides) — this is already listed in `package.json`, so `npm install` should have handled it, but if prompted, just accept.

### Export Lecture 1 to PDF

```bash
npm run export:lecture-01
```

This produces `lecture-01-introduction/lecture-01-introduction.pdf`.

### Export Lecture 1 to PowerPoint (.pptx)

```bash
npm run export:lecture-01:pptx
```

This produces `lecture-01-introduction/lecture-01-introduction.pptx`. Note that PPTX export embeds each slide as an image (not editable text/shapes) — it's meant for sharing/printing, not for further editing in PowerPoint.

### Exporting any lecture manually

If a lecture doesn't have a dedicated script yet, export it directly:

```bash
npx slidev export lecture-02-whatever/slides.md --output lecture-02-whatever/lecture-02.pdf
npx slidev export lecture-02-whatever/slides.md --format pptx --output lecture-02-whatever/lecture-02.pptx
npx slidev export lecture-02-whatever/slides.md --format png --output lecture-02-whatever/slides
```

Other handy export flags:

- `--with-clicks` — export a separate page/slide for every click/reveal step (useful since these decks use `v-click`)
- `--dark` — export using dark mode
- `--range 1,4-6` — export only specific slides

Full reference: [Slidev exporting docs](https://sli.dev/guide/exporting).

## 5. Building a shareable static website

To turn a deck into a standalone website (e.g. to host on GitHub Pages) instead of a PDF:

```bash
npm run build:lecture-01
```

This outputs static HTML/JS/CSS into `lecture-01-introduction/dist/`, which you can deploy anywhere (Netlify, Vercel, GitHub Pages, etc.).

---

## Adding a new lecture

1. Create a new folder following the naming pattern: `lecture-02-<short-title>/`
2. Add `slides.md` inside it (copy an existing lecture's frontmatter as a starting template)
3. If it needs custom styling, add a `style.css` in the same folder (Slidev auto-loads it)
4. Put any images in a `assets/` subfolder and reference them as `./assets/filename.png`
5. Add two scripts to the root `package.json` (dev + PDF export), following the same pattern as Lecture 1
6. Commit and push

---

## Troubleshooting

**"Import ... resolves outside of Vite server.fs.allow" error on Windows**
This happens if an image is referenced with a leading slash (e.g. `/assets/img.png`) instead of a relative path. All images in these decks use `./assets/...` (relative), which avoids this issue — if you add new images, keep using the relative path style.

**Slide content gets cut off / doesn't fit**
Slidev slides have a fixed height and don't scroll. If a slide has too much content, split it into two slides rather than shrinking text indefinitely — see how the existing decks split dense topics (e.g. tables, multi-part examples) across two slides.

**`npm install` fails or is slow**
Make sure you're on Node.js ≥ 20.12.0. Deleting `node_modules/` and `package-lock.json` and re-running `npm install` usually resolves stale-dependency issues.

---

## License / Attribution

Course: **DSAI 403 — Nature Inspired Computation**
Zewail City of Science, Technology, and Innovation