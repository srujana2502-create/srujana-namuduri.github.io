# Portfolio — Sai Srujana Namuduri

Simple static HTML portfolio for GitHub Pages.

## Deploy to GitHub Pages

1. **Create a new GitHub repo** named `srujana-namuduri.github.io` (or `your-username.github.io`).
2. **Copy the contents** of this folder into the repo root. The repo root should contain:
   - `index.html`
   - `css/`
   - `images/`
   - `projects/`
3. **Push** to the `main` branch.
4. **Enable GitHub Pages:**
   - Go to repo **Settings** → **Pages**
   - Under **Source**, select **Deploy from a branch**
   - Branch: `main` (or `master`)
   - Folder: `/ (root)`
   - Click **Save**
5. Your site will be live at `https://srujana-namuduri.github.io` within a few minutes.

## Optional: Add resume PDF

1. Export a PDF from `resume-Srujana-Namuduri-export.html` (open in browser → File → Print → Save as PDF).
2. Save as `resume.pdf` in this folder.
3. Update `index.html` Resume section: add `<a href="resume.pdf" class="resume-link" download>Download Resume (PDF)</a>`.

## Local preview

Open `index.html` in a browser, or run a simple server:

```bash
cd portfolio
python3 -m http.server 8000
```

Then visit http://localhost:8000
