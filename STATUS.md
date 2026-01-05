# Website Status

**Last Updated:** January 5, 2026  
**Status:** ✅ Site complete and ready for deployment

---

## Site Structure

The site is organized with the following pages:

- **Home** (`index.qmd`) - Bio and photo
- **Publications** (`publications.qmd`) - Published papers with PDFs and journal links
- **Working Papers** (`working-papers.qmd`) - Working papers index with landing pages
- **CV** (`cv.qmd` + `cv-pdf.qmd`) - HTML CV with downloadable PDF
- **Contact** (`links.qmd`) - Email, address, and academic profile links

---

## Working Papers

Three working papers have dedicated landing pages with Google Scholar meta tags:

1. **Minimum Wages, Inequality, and the Informal Sector** (`papers/minwage-inequality.qmd`)
   - R&R at American Economic Review
   
2. **Subjective Beliefs, Disagreement, and Market Return Predictability** (`papers/ibes-market-returns.qmd`)
   - Revision requested at Critical Finance Review
   
3. **Monetary Policy and Labor Markets in a Developing Economy** (`papers/monetary-policy-heterogeneity.qmd`)
   - Revision requested at Journal of Money, Credit, and Banking

Each has proper `citation_*` meta tags for Google Scholar indexing.

---

## File Organization

```
website/
├── _quarto.yml              # Site configuration
├── custom.scss              # FGV styling
├── index.qmd                # Home page
├── publications.qmd         # Publications list
├── working-papers.qmd       # Working papers index
├── cv.qmd                   # HTML CV
├── cv-pdf.qmd              # PDF CV source
├── links.qmd               # Contact page
├── assets/
│   ├── portrait.jpg        # Profile photo
│   └── favicon.svg         # Site icon
├── papers/
│   ├── *.pdf               # Publication PDFs
│   └── *.qmd               # Working paper landing pages
└── working_papers/
    └── *.pdf               # Working paper PDFs
```

---

## Documentation

- **README.md** - Quick start guide and deployment instructions
- **AGENTS.md** - Role-based agent guidance for AI assistants
- **DEPLOYMENT.md** - Detailed deployment instructions
- **WORKING_PAPER_INSTRUCTIONS.md** - Comprehensive guide for adding working papers
- **AGENT_QUICK_START.md** - Quick reference for adding working papers

---

## Next Steps

### For Deployment

1. Review the site locally with `quarto preview`
2. Deploy to GitHub Pages with `quarto publish gh-pages`
3. Verify all links work in production
4. (Optional) Add Google Analytics in `_quarto.yml`

### For Maintenance

- **Adding a new publication:** Edit `publications.qmd`
- **Adding a new working paper:** See `WORKING_PAPER_INSTRUCTIONS.md`
- **Updating CV:** Edit `cv.qmd` and `cv-pdf.qmd`, then render

---

## Notes

- Site uses FGV brand colors (blue: #1C2F67)
- All pages are mobile-responsive
- Google Scholar meta tags implemented for working papers
- PDFs hosted locally for stable links
- Clean, professional design matching original Google Sites

**Site is ready for deployment!**

