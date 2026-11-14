# Portfolio Site v2

## What this is
A static HTML/CSS/JS portfolio site for Christopher Costes, cloned from the live Squarespace site at christophercostes.com. No framework, no build tools — just plain HTML files served locally.

## Running locally
```bash
python3 -m http.server 8001
# Open http://localhost:8001
```

## Project structure
- **22 HTML pages** in the root directory (index, work, bio, publications, anecdotes, plus individual case studies and experiments)
- `assets/styles.css` — all CSS
- `assets/main.js` — all JS
- `assets/images/<page-name>/` — locally hosted images per page

## Key conventions
- All image paths are local (`assets/images/...`), not Squarespace CDN URLs
- Nav links: Work, Publications, Experiments, Bio, Resume — consistent across all pages
- "Experiments" in the nav links to `anecdotes.html` (the URL slug kept from Squarespace)
- Case study image layouts use classes: `.case-study-image`, `.case-study-image-grid`, `.case-study-hero-image`, `.case-study-section-banner`
- Resume links point to `christophercostes.com/s/Christopher_Costes_Designer.pdf` (external, on Squarespace)

## GitHub
- Repo: https://github.com/Tophcostes/portfolio-site-v2
- Remote: `origin` → `portfolio-site-v2.git`

## Known issues (from Phase 1 audit)
- **Homepage mobile spacing**: large gap between "Recent Work" label and the first work card at mobile widths
- **Case study text contrast**: on mobile, case study page hero text is nearly invisible (very light gray)
- **Live site has diverged**: the live christophercostes.com now has a dark hero with sketch background, CC logo, underlined keywords, and different card layout — the clone reflects an older version of the design

## Reference
- Live site: https://www.christophercostes.com
- Squarespace CDN pattern: `https://images.squarespace-cdn.com/content/v1/5fffe215879bf154c30dd438/`
