# Editing this website

Everything here is plain HTML and one CSS file. There is no build step, no framework,
and nothing to install. You edit a file, save it, and push.

---

## One-time setup

Clone the repo somewhere permanent:

```bash
git clone https://github.com/matthewgoodbred/matthewgoodbred.github.io.git ~/Documents/website
```

Tell git who you are (only needed once, ever):

```bash
git config --global user.name "Matthew Goodbred"
git config --global user.email "matthew.goodbred@gmail.com"
```

Authentication is already handled — your GitHub token is in the macOS Keychain, so
`git push` works without prompting.

---

## The loop

Three steps, every time.

**1. Preview locally.** From the repo folder:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Leave it running while you work; just refresh the
browser after each save. Stop it with Ctrl-C.

**2. Edit.** Open the `.html` files in any text editor. They are ordinary HTML — the
prose is sitting right there in `<p>` tags and you can type over it.

**3. Publish.**

```bash
git add -A
git commit -m "say what you changed"
git push
```

The live site updates about a minute later. Hard-refresh (Cmd-Shift-R) if you still see
the old version — that is your browser's cache, not a failed deploy.

---

## Where things live

| I want to change... | Edit this |
|---|---|
| Bio, personal interests | `index.html` |
| Research sections | `research.html` |
| Papers and their descriptions | `publications.html` |
| CV contents | `cv.html` |
| Colors, fonts, spacing | `assets/css/style.css` |
| Photos and figures | files in `assets/img/` |
| Downloadable CV | `assets/cv/Goodbred_CV.pdf` |

The nav bar, footer, and contact block are repeated in all four HTML files. If you change
one, change all four — that is the one cost of having no build step.

---

## Common tasks

### Change some text

Find the sentence in the `.html` file and type over it. Leave the tags alone:

```html
<p>
  I am a Ph.D. student in the Department of ...   <!-- edit inside here -->
</p>
```

### Replace a photo or figure

Put your file in `assets/img/`, then point the `src` at it:

```html
<img src="assets/img/portrait.jpg" alt="Matthew Goodbred">
```

Keep the `alt` text accurate — it is what screen readers announce and what shows if the
image fails to load.

**Resize before committing.** A 4000px camera JPEG makes the page slow for no visible
benefit. 1600px on the long edge is plenty:

```bash
sips --resampleWidth 1600 ~/Desktop/photo.jpg --out assets/img/hiking-1.jpg
```

### Fill a placeholder slot

Empty slots render as dashed grey boxes naming the file they expect. To fill one, replace
the whole `<div class="placeholder">...</div>` with an `<img>`:

```html
<!-- before -->
<div class="placeholder">Add a photo at<br>assets/img/hiking-1.jpg</div>

<!-- after -->
<img src="assets/img/hiking-1.jpg" alt="Descriptive alt text">
```

To remove a slot you do not want, delete the whole `<figure>` block around it.

### Add a publication

Open `publications.html`. There is a commented-out template at the top of the list —
copy it, paste it above the newest paper, fill it in. Author order top to bottom matches
display order.

### Add a research section

Copy an existing `<section>` in `research.html` and change the `id`, heading, and body.
The `id` is what lets you link straight to it, e.g. `research.html#magnetic-reconnection`.

### Embed another video

Take the YouTube id from the URL — in `youtube.com/watch?v=nO2B5gv5Gww` the id is
`nO2B5gv5Gww` — and drop it into this block:

```html
<div class="video">
  <iframe src="https://www.youtube-nocookie.com/embed/YOUR_ID_HERE"
          title="Describe the video" loading="lazy" allowfullscreen></iframe>
</div>
```

### Change the look

Every color, font, and width is a variable at the top of `assets/css/style.css`:

```css
:root {
  --accent: #1f5c8b;   /* link and underline color */
  --measure: 44rem;    /* how wide paragraphs get  */
  ...
}
```

Change the value once and it updates everywhere.

### Update the CV

Replace `assets/cv/Goodbred_CV.pdf` with your newly compiled PDF, keeping the filename
identical so the download link still works. Then update `cv.html` to match — the page and
the PDF should never disagree.

---

## If something breaks

Nothing here can break permanently — every version is in git.

Undo your edits to one file, before committing:

```bash
git checkout -- index.html
```

Undo everything since the last commit:

```bash
git reset --hard
```

Go back to how the site looked at some earlier commit:

```bash
git log --oneline          # find the commit you want
git revert <commit-sha>    # makes a new commit undoing that one
git push
```

If a page renders wrong, it is almost always an unclosed tag. Paste the file into
<https://validator.w3.org/nu/> and it will point at the line.
