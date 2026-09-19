# matthewgoodbred.github.io

Personal academic website — plain static HTML and one stylesheet. No build step, no
dependencies. Open `index.html` in a browser to preview, or serve the folder:

```bash
python3 -m http.server 8000
```

## Layout

```
index.html          About + personal interests
research.html       Research interests (pulsar magnetospheres, magnetic reconnection)
publications.html   Publication list with descriptions and figures
cv.html             Full CV
assets/css/style.css   All styling (design tokens at the top under :root)
assets/img/            Figures and photos
assets/cv/             cv.tex source; put the compiled PDF here as Goodbred_CV.pdf
```

## Adding things

**A photo or figure** — drop the file in `assets/img/` and point the `<img src>` at it.
Slots waiting for content are marked with a dashed `placeholder` box; each one names the
filename it expects.

**A publication** — copy the commented-out template block at the top of
`publications.html` and fill it in.

**A research section** — copy a `<section>` from `research.html`; give it an `id` so it
can be linked directly.

**Colors, fonts, widths** — every value lives in the `:root` block at the top of
`assets/css/style.css`.

## Deploying to GitHub Pages

Pages is configured to deploy from `main` / `/ (root)`, so pushing to `main` publishes
the site at <https://matthewgoodbred.github.io/>. Give it a minute after each push.

The repo name must stay `matthewgoodbred.github.io` — that exact name is what makes
GitHub serve it at the bare domain rather than under a subpath.
