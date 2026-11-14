# Portfolio Test Site — Project Handover

**Session date:** 2026-11-14  
**GitHub repo:** https://github.com/Tophcostes/portfolio-test-site  
**Live reference site:** https://www.christophercostes.com  
**Local dev:** `python3 -m http.server 8000` (from project root), then open http://localhost:8000

---

## What This Project Is

A static HTML/CSS/JS clone of christophercostes.com, built without any framework or build tool. All assets are hosted locally inside the project. The goal is a fully self-contained, locally-runnable portfolio site that mirrors the live Squarespace site.

---

## Completed Work

### Infrastructure
- [x] Public GitHub repo created and connected (`Tophcostes/portfolio-test-site`)
- [x] README written describing site structure, pages, and how to run locally
- [x] All 22 HTML pages exist and are linked correctly

### Image Rollout (the main body of work)
All images were downloaded from the live Squarespace CDN and stored locally under `assets/images/`. HTML files were updated to reference local paths. Pages completed:

| Page | Images | Local Directory |
|------|--------|----------------|
| index.html | 4 | assets/images/home/ |
| work.html | 7 thumbnails | assets/images/work-thumbnails/ |
| work-lyftotto.html | 49 (inc. GIFs) | assets/images/work-lyftotto/ |
| work-theleague.html | 29 | assets/images/work-theleague/ |
| work-ontra.html | 14 | assets/images/work-ontra/ |
| work-complianceai.html | 10 | assets/images/work-complianceai/ |
| work-remark.html | 12 | assets/images/work-remark/ |
| work-academic-coaching.html | 16 | assets/images/work-academic-coaching/ |
| work-embeddedbanking.html | 6 | assets/images/work-embeddedbanking/ |
| anecdotes.html | 10 thumbnails | assets/images/anecdotes-thumbnails/ |
| anecdotes-mycelium-connections.html | 3 | assets/images/anecdotes-mycelium/ |
| anecdotes-thegoodmeal.html | 9 | assets/images/anecdotes-thegoodmeal/ |
| anecdotes-plastic-world.html | 2 | assets/images/anecdotes-plastic-world/ |
| anecdotes-physical-design.html | 8 | assets/images/anecdotes-physical-design/ |
| anecdotes-mckinsey.html | 2 | assets/images/anecdotes-mckinsey/ |
| anecdotes-post-series.html | 21 | assets/images/anecdotes-post-series/ |
| anecdotes-magic-thinking.html | 6 | assets/images/anecdotes-magic-thinking/ |
| anecdotes-fake-news-visualization.html | 2 | assets/images/anecdotes-fake-news/ |
| bio.html | 2 | assets/images/bio/ |
| publications.html | 6 | assets/images/publications/ |

### CSS Additions (`assets/styles.css`)
New classes added for case study image layouts:
```css
.case-study-image           /* single full-width image */
.case-study-image-grid      /* grid container */
.case-study-image-grid.cols-2 / .cols-3 / .cols-4
.case-study-hero-image      /* hero banner image */
.case-study-section-banner  /* section divider image */
.card-img img               /* thumbnail card images */
```

### Bugs Fixed
- **publications.html curly quote bug:** `src` attributes had Unicode curly quotes (`"` `"`) instead of ASCII `"`, causing browsers to request URL-encoded paths like `%E2%80%9Dpublications-header.png%E2%80%9D` → 404. Fixed by replacing all smart quotes with straight ASCII quotes.
- **index.html wrong filenames:** Had `home/card-jpmorgan.png` etc. → corrected to `home/jpmorgan.png`
- **bio.html missing file:** Referenced `bio/teamwork.jpg` (didn't exist) → corrected to `bio/img-02.jpg`
- **CSS linter mangling:** After bulk edits, nth-child rules were duplicated → restored manually

---

## Incomplete / Not Yet Done

### Two anecdotes pages have no body images yet
These pages exist and load, but their image directories are empty. Only a thumbnail image (on the anecdotes index) exists for each.

| Page | Missing images from |
|------|-------------------|
| anecdotes-laundry-machine-ui.html | assets/images/anecdotes-laundry-machine/ |
| anecdotes-metaphor-animation.html | assets/images/anecdotes-metaphor-animation/ |

**What to do:** Visit the live pages on christophercostes.com, find the image URLs (inspect element → `src`), download them into the respective folders, and add `<img>` tags to the HTML.

### No navigation / global header tested across all pages
The HTML was cloned from a Squarespace export and may have inconsistencies in nav links between pages. Not fully audited.

### No mobile testing done
The site uses responsive CSS but it has not been tested at mobile viewport widths in this session.

---

## Actions Needed to Replicate This in Another Project ("Anti Gravity")

To bring a new/different project to the same state as this one, work through these steps in order:

### 1. Set up the GitHub repo
```bash
gh repo create <repo-name> --public --source=. --remote=origin --push
```

### 2. Download images from the live site
For each page, use the browser's DevTools (Elements tab) to find `<img src="...">` values on the live Squarespace site. Download them:
```bash
mkdir -p assets/images/<page-name>
curl -o assets/images/<page-name>/filename.ext "https://images.squarespace-cdn.com/..."
```
For many images in parallel:
```bash
curl -o file1.png "url1" &
curl -o file2.jpg "url2" &
wait
```

### 3. Replace placeholder `<div class="card-img"></div>` with real images
After downloading, update the HTML. For work/anecdotes thumbnail cards:
```html
<div class="card-img"><img src="assets/images/<folder>/filename.ext" style="width:100%;height:100%;object-fit:cover;display:block;"></div>
```
For case study body images, use the CSS classes added in this project:
```html
<div class="case-study-image"><img src="assets/images/.../filename.ext" alt="Description"></div>
```

### 4. Add CSS classes if not already present
Copy the image layout classes listed above from `assets/styles.css` in this project into the new project's stylesheet.

### 5. Watch for the curly quote trap
If any HTML was generated by an AI tool or copied from a rich-text editor, check that `src="..."` attributes use straight ASCII double quotes (`"`), not curly smart quotes (`"` `"`). To fix:
```python
html = open('page.html', encoding='utf-8').read()
html = html.replace('“', '"').replace('”', '"')
open('page.html', 'w', encoding='utf-8').write(html)
```

### 6. Verify locally before pushing
```bash
python3 -m http.server 8000
# Open http://localhost:8000 and check each page
# Watch the terminal for 404s — they reveal broken image paths
```

### 7. Commit and push
```bash
git add .
git commit -m "Add images and update HTML paths"
git push
```

---

## Useful Reference

- **Live site:** https://www.christophercostes.com
- **GitHub repo:** https://github.com/Tophcostes/portfolio-test-site
- **Squarespace CDN base URL pattern:** `https://images.squarespace-cdn.com/content/v1/5fffe215879bf154c30dd438/`
- **Local server:** `python3 -m http.server 8000` → http://localhost:8000
