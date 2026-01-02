# Website Migration TODO List

## High Priority Tasks

### 1. Site Structure Reorganization

- [x] **Split Research page into two separate pages**
  - [x] Create `publications.qmd` for peer-reviewed published papers
  - [x] Create `working-papers.qmd` for working papers and works in progress
  - [x] Update navbar in `_quarto.yml` to include both pages
  - [x] Remove old `research.qmd`

### 2. Contact & Identity Page

- [x] **Create unified contact/links page** (`links.qmd`, labeled “Contact” in navbar)
  - [x] Include email and mailing address
  - [x] Add Google Scholar link
  - [x] Add Lattes CV link
  - [x] Add ORCID link
  - [x] Add RePEc/IDEAS link
  - [ ] Add SSRN link (optional, if applicable)
  - [ ] Add GitHub link (optional, if applicable)
  - [x] Update navbar to include this page

### 3. Publications Content

- [x] **Import PDFs from old website** (or other sources)
  - [x] Download/collect PDFs for all 9 published papers:
    - [x] "Housing supply in the presence of informality" (2023)
    - [x] "Underdiversification and idiosyncratic risk externalities" (2022)
    - [x] "Information quality and regime change: Evidence from the lab" (2021)
    - [x] "The choice channel of financial innovation" (2021)
    - [x] "Earning dynamics with a large informal sector" (2020)
    - [x] "Competitive real options under private information" (2020)
    - [x] "Capital budgeting and risk taking under credit constraints" (2020)
    - [x] "Homicides and the age of criminal responsibility in Brazil" (2018)
    - [x] "Information quality and crises in regime-change games" (2015)
  - [x] Place PDFs in `/papers/` directory
  - [x] Update links in `publications.qmd` to point to local PDFs
  - [x] Keep journal links for published versions

### 4. Working Papers

- [x] **Create dedicated landing pages** for each public working paper (in `/papers/`)
  - [x] Include proper Google Scholar meta tags (`citation_*`)
  - [x] Store working paper PDFs in `/working_papers/` and link directly
  - [x] Include status (R&R, revision requested, etc.)
- [x] **Update `working-papers.qmd`** index page
  - [x] List each working paper with `[page]` and `[pdf]` links
- [ ] **Add/maintain additional working papers** as they become public (optional/ongoing)

### 5. CV Fixes

- [x] **Fix HTML CV rendering** (`cv.qmd`)
  - [x] Improve visual appearance and layout
  - [x] Test responsive design

- [ ] **(Optional) Update CV content from Lattes**
  - [ ] Add a “last updated” date (HTML + PDF header)

- [x] **Verify PDF CV** (`cv-pdf.qmd`)
  - [x] Compiles and download link works

## Medium Priority Tasks

### 6. Google Scholar Indexing

- [ ] **Ensure proper meta tags** on all pages
- [ ] **Verify sitemap** generation after deploy
- [ ] **Test working paper pages** have correct citation meta tags
- [ ] **Add Google Scholar link** to navbar or identity page

### 7. Analytics & Migration

- [ ] **Add GA4 Measurement ID** in `_quarto.yml`
  - [ ] Get/reuse existing GA4 property if available
  - [ ] Configure analytics
- [ ] **Create migration notice** for old Google Sites
  - [ ] Draft short text pointing to new domain
  - [ ] Note: This will be a manual step on Google Sites

### 8. Content Verification

- [ ] **Review all internal links** to ensure they work
- [ ] **Check all external links** (journal links, institutional links)
- [ ] **Verify all PDF links** work correctly
- [ ] **Test site on mobile devices**

## Low Priority / Nice to Have

### 9. Design Polish

- [ ] Review color scheme consistency
- [ ] Check typography across all pages
- [ ] Optimize images (profile photo, etc.)
- [ ] Add favicon if not already present

### 10. Documentation

- [ ] Update README.md with site information
- [ ] Document how to add new publications
- [ ] Document how to add new working papers
- [ ] Note deployment process

## Current Status

### ✅ Completed

- ✅ Basic site structure implemented
- ✅ SCSS layer boundaries fixed
- ✅ Site renders successfully
- ✅ Preview server running on port 4200
- ✅ **Split Research into Publications and Working Papers pages**
- ✅ **Updated navbar with Publications and Working Papers**
- ✅ **Created Links/Contact page (links.qmd)**
- ✅ **Fixed CV HTML rendering** - improved styling and layout
- ✅ **Removed Selected Publications from home page** - cleaner design
- ✅ **Downloaded portrait from original site** (assets/portrait.jpg)
- ✅ Initial CV structure
- ✅ Publications listed (needs PDF imports)
- ✅ Working paper template created
- ✅ Publication PDFs added to `/papers/` and linked from `publications.qmd`
- ✅ Working paper PDFs in `/working_papers/` + landing pages in `/papers/`

### 🔄 In Progress

- 🔄 Documentation refresh + optional maintenance items (analytics, “last updated” dates)

## Notes

- Prefer Lattes as canonical source for CV facts when conflicts arise
- Keep working paper PDFs under `/working_papers/` directory for stable links
- Use simple Markdown, avoid JS dependencies
- Minimal CSS changes: only in custom.scss
- All pages should have proper Google Scholar meta tags

## Questions to Resolve

- [ ] Do you want GA4 analytics? If yes, what is the Measurement ID?
- [ ] Should we add optional links on `links.qmd` (SSRN / GitHub)?
