# elizabethsforbes.github.io — site source

A minimal, photo-forward static site for academic use, built as a prototype to replace the Wix site at
[forbeselizabeths.wixsite.com/elizabethsforbes](https://forbeselizabeths.wixsite.com/elizabethsforbes).

No build step, no Jekyll, no Ruby. Pages are plain HTML so you can edit any of them in any text editor
and see the change by reloading your browser. When you're ready, push to GitHub and turn on Pages.

---

## File map

```
website/
├── index.html          ← Home / About (the hero photo + bio)
├── research.html       ← Research overview + project cards
├── publications.html   ← Papers grouped by year
├── teaching.html       ← Teaching, mentoring, outreach, service
├── news.html           ← Reverse-chronological updates
├── cv.html             ← On-page CV summary; links to PDF
├── assets/
│   ├── css/style.css   ← All styles. Edit colors/fonts at the top.
│   ├── img/            ← Drop your photos here (hero.jpg, project-1.jpg, …)
│   └── files/          ← Drop forbes-cv.pdf and any other downloads here
└── README.md           ← This file
```

---

## Preview locally

You can either:

**(A) Just double-click `index.html`** to open it in your browser. Everything works except links that point to other pages, which need a server.

**(B) Run a tiny local server** so navigation between pages works:

```bash
cd website
python3 -m http.server 8000
# now visit http://localhost:8000
```

Reload the page after every save.

---

## Deploy to GitHub Pages (one-time setup)

1. **Make a GitHub account** if you don't already have one: <https://github.com/signup>.
2. **Create a new repository** named exactly `YOUR_USERNAME.github.io` (replace `YOUR_USERNAME` with your GitHub username — the repo name must match this format for the free, custom-URL flavor of GitHub Pages).
3. **Upload the contents of this `website/` folder to the repo.** The simplest way:
   - On the new empty repo page, click "uploading an existing file."
   - Drag every file and folder *inside* `website/` (not the `website/` folder itself).
   - Commit.
4. In the repo's **Settings → Pages**, set **Source: Deploy from a branch**, **Branch: `main`**, **Folder: `/ (root)`**, then save.
5. Wait ~1 minute. Your site is live at `https://YOUR_USERNAME.github.io/`.

If you prefer the command line:

```bash
cd website
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_USERNAME.github.io.git
git push -u origin main
```

### Custom domain (optional)

If you own a domain like `elizabethforbes.com`:
1. Add a file named `CNAME` in the repo root containing just the domain (e.g. `elizabethforbes.com`).
2. In your domain registrar, point an `A` or `CNAME` record at GitHub Pages (instructions: <https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site>).

---

## How to update content

Almost all edits are find-and-replace inside the HTML files. Each file has `<!-- EDIT: ... -->` comments wherever there's placeholder text — search for `EDIT` to see every spot to update.

### Add a new publication

Open `publications.html`, find the year, copy one `<li class="pub-item">` block, paste it under the year, and update the title/authors/venue/links. Wrap your name in `<span class="me">…</span>` so it bolds.

### Add a news item

Open `news.html`. Copy a `<div class="news-item">` block and put it at the **top** of the list. Update the date and text.

### Add a project to the research page

Open `research.html`. Copy an `<article class="project">` block inside `.project-grid`. Update the title, description, and the photo path: `style="background-image:url('assets/img/your-photo.jpg');"`.

### Replace the hero photo

Drop a JPG or PNG named `hero.jpg` into `assets/img/`. The file path is referenced in `assets/css/style.css` (line near the top, under `.hero-photo`). Aspect ratio of roughly 4:5 (portrait) works best.

### Update colors / fonts

Open `assets/css/style.css`. The very top has a `:root { ... }` block with all colors and fonts as variables. Change `--accent` to recolor the whole site.

### Update navigation

The nav is repeated at the top of every `.html` file (since there's no build step). If you add a new page, copy the nav into it and update the links in **all** files — a quick find-and-replace in your editor handles it. Mark the current page's link with `class="active"`.

---

## Things you'll want to change before going live

Search the codebase for these and replace:

- `YOUR_USERNAME` — your GitHub username (in footer + Scholar/ORCID/etc. links)
- `YOUR_ID` — your Google Scholar profile ID
- `0000-0000-0000-0000` — your ORCID
- `forbeselizabeth.s@gmail.com` — confirm the email you want public (same one you use now is fine)
- All the `<!-- EDIT: ... -->` placeholder text in each page
- Replace files in `assets/img/` and `assets/files/forbes-cv.pdf` with your real ones

---

## Why this stack vs. al-folio / academicpages?

You said no strong preference, so I picked the path of least resistance:

- **This setup (plain HTML on GitHub Pages):** Zero build step. Edit a file, refresh, see the change. Add a publication by copying ten lines. The cost is that adding a new section of pages means duplicating the nav.
- **al-folio / academicpages (Jekyll on GitHub Pages):** What your colleagues use. More elegant for adding new posts/papers via Markdown + YAML, automatic nav, BibTeX support. The cost is a steeper learning curve and a Ruby toolchain to preview locally.

If after a couple months you find yourself wanting BibTeX-driven publications or a real blog with tags, ping me and I'll port this design into a Jekyll/al-folio repo with the same look. The visual design carries over.
