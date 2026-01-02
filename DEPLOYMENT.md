# Deployment Guide

## Overview

This website uses a **single repository** approach where documentation files exist in the repo but are excluded from the published website.

## What Gets Published

The website is rendered to the `_site/` directory, which contains only:
- HTML pages from `.qmd` files
- PDFs from `/papers/` and `/working_papers/`
- CSS and assets
- Supporting JavaScript libraries

## What Stays Private (In Repo Only)

These files exist in your GitHub repository but are **NOT rendered** or published:

- `AGENTS.md` - Agent role definitions
- `PROGRESS.md` - Progress tracking
- `TODO.md` - Task list
- `TASK_COMPLETED.md` - Completion summary
- `WORKING_PAPER_INSTRUCTIONS.md` - Full guide for adding papers
- `AGENT_QUICK_START.md` - Quick reference for agents
- `DEPLOYMENT.md` - This file
- `README.md` - Repository documentation

These files are configured in `_quarto.yml` under `project.render` to be excluded.

## Repository Structure

```
website/
├── .gitignore           # Excludes _site/, .quarto/, etc.
├── _quarto.yml          # Site config (excludes documentation from rendering)
├── _site/               # Generated site (gitignored, published separately)
│
├── *.qmd                # Content pages (rendered to HTML)
├── papers/              # PDFs and landing pages
├── working_papers/      # Working paper PDFs
├── assets/              # Images, etc.
│
└── [Documentation]      # In repo, NOT rendered:
    ├── AGENTS.md
    ├── PROGRESS.md
    ├── TODO.md
    ├── WORKING_PAPER_INSTRUCTIONS.md
    └── etc.
```

## How to Deploy

### Option 1: GitHub Pages (Recommended)

1. **Create GitHub Repository**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/yourusername/yourrepo.git
   git push -u origin main
   ```

2. **Set Up GitHub Actions** (Automatic Deployment)
   
   Create `.github/workflows/publish.yml`:
   
   ```yaml
   name: Publish Quarto Site
   
   on:
     push:
       branches: [main]
     workflow_dispatch:
   
   jobs:
     build-deploy:
       runs-on: ubuntu-latest
       permissions:
         contents: write
       steps:
         - uses: actions/checkout@v4
         
         - name: Set up Quarto
           uses: quarto-dev/quarto-actions/setup@v2
         
         - name: Render site
           run: quarto render
         
         - name: Deploy to GitHub Pages
           uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./_site
   ```

3. **Enable GitHub Pages**
   - Go to repository Settings → Pages
   - Source: Deploy from a branch
   - Branch: `gh-pages` (created by the action)
   - Folder: `/ (root)`
   - Save

4. **Update Site URL**
   
   Edit `_quarto.yml`:
   ```yaml
   website:
     site-url: https://yourusername.github.io/yourrepo
   ```
   
   Also update all `citation_pdf_url` in working paper landing pages to match.

### Option 2: Manual Deploy

1. **Render the site locally**
   ```bash
   quarto render
   ```

2. **Push _site/ to gh-pages branch**
   ```bash
   cd _site
   git init
   git add .
   git commit -m "Deploy site"
   git branch -M gh-pages
   git remote add origin https://github.com/yourusername/yourrepo.git
   git push -f origin gh-pages
   ```

3. **Enable GitHub Pages** (as in Option 1, step 3)

### Option 3: Other Hosting

The `_site/` directory is a complete static website. You can:
- Upload to Netlify (drag & drop `_site/`)
- Deploy to Vercel
- Upload to any web server via FTP/SFTP

## Before First Deploy

### Update Configuration

1. **Site URL** in `_quarto.yml`:
   ```yaml
   website:
     site-url: https://your-actual-domain.com
   ```

2. **PDF URLs** in all working paper landing pages:
   - `/papers/minwage-inequality.qmd`
   - `/papers/ibes-market-returns.qmd`
   - `/papers/monetary-policy-heterogeneity.qmd`
   
   Update the `citation_pdf_url` to match your deployed domain:
   ```yaml
   <meta name="citation_pdf_url" content="https://your-actual-domain.com/working_papers/filename.pdf">
   ```

### Test Locally

```bash
quarto preview
```

Visit http://localhost:4200 and verify:
- All pages load correctly
- All links work
- PDFs download properly
- Working paper landing pages display correctly

## Post-Deploy Checklist

- [ ] All pages accessible
- [ ] No broken links
- [ ] PDFs download correctly
- [ ] Working paper landing pages have correct meta tags (view source)
- [ ] Google Scholar meta tags present (search for "citation_" in page source)
- [ ] Site appears in Google Scholar within 1-2 weeks
- [ ] Documentation files NOT visible on website (only in repo)
- [ ] Analytics tracking (if configured)

## Updating the Site

1. Make changes to `.qmd` files or other content
2. Commit and push to `main` branch
3. GitHub Actions will automatically rebuild and deploy (if using Option 1)
4. If manual: run `quarto render` and re-deploy `_site/`

## Google Scholar Indexing

After deployment:
- Wait 1-2 weeks for Google Scholar to crawl your site
- Search for your papers on Google Scholar to verify indexing
- Check that paper landing pages show up in search results
- Verify citations link back to your PDFs

## Troubleshooting

### Documentation Files Appearing on Website

If you see `.md` files on the published site:
- Check `_quarto.yml` has the `render` exclusions
- Run `quarto render` again
- Clear browser cache

### PDFs Not Loading

- Check relative paths are correct
- Verify PDFs exist in `/working_papers/` directory
- Check capitalization (Linux/Mac are case-sensitive)

### Google Scholar Not Indexing

- View page source and verify meta tags are present
- Ensure `citation_pdf_url` is absolute (https://...)
- Check PDFs are publicly accessible (no login required)
- Allow 1-2 weeks for crawling

## Files Reference

### Rendered to Website ✓
- `index.qmd`, `cv.qmd`, `publications.qmd`, `working-papers.qmd`, `links.qmd`
- `/papers/*.qmd` (working paper landing pages)
- All PDFs in `/papers/` and `/working_papers/`
- `custom.scss`, `styles.css`
- `/assets/*`

### In Repo Only (Not Published) ✗
- `AGENTS.md`
- `PROGRESS.md`
- `TODO.md`
- `TASK_COMPLETED.md`
- `WORKING_PAPER_INSTRUCTIONS.md`
- `AGENT_QUICK_START.md`
- `DEPLOYMENT.md`
- `README.md`
- `.gitignore`, `.quartoignore`
- `_quarto.yml` (config only, not rendered as page)

### Build Artifacts (gitignored) 🚫
- `_site/` - Generated website
- `.quarto/` - Quarto cache
- `_freeze/` - Frozen computational results

## Support

For questions about:
- **Quarto**: https://quarto.org/docs/
- **GitHub Pages**: https://docs.github.com/pages
- **Google Scholar**: https://scholar.google.com/intl/en/scholar/inclusion.html

---

**Last Updated:** January 2, 2026

