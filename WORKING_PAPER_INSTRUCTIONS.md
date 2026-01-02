# Working Paper Landing Page Instructions

## Purpose

This guide helps AI agents (or humans) create landing pages for working papers on this academic website. Landing pages serve two critical functions:

1. **Google Scholar Indexing**: Meta tags enable Google Scholar to index the paper
2. **Professional Presentation**: Provides context, status, and author information

## Prerequisites

Before creating a landing page, you need:

1. **PDF file** of the working paper (placed in `/working_papers/` directory)
2. **Paper metadata**:
   - Full title
   - All author names and affiliations
   - Publication/last update year
   - Abstract (at least a brief one)
   - Current status (e.g., "R&R at Journal X", "Working Paper", "Under Review")

**Repo conventions (this site):**
- **Published-paper PDFs** live in `/papers/` and are linked from `publications.qmd`
- **Working-paper PDFs** live in `/working_papers/` and are linked from `working-papers.qmd`
- **Working-paper landing pages** live in `/papers/*.qmd` (these carry Google Scholar `citation_*` meta tags)

## Step-by-Step Process

### Step 1: Choose a Filename

Create a short, URL-friendly slug for the paper filename:
- Use lowercase letters
- Replace spaces with hyphens
- Keep it short but descriptive
- No special characters except hyphens

**Examples:**
- "Minimum Wages, Inequality, and the Informal Sector" → `minwage-inequality.qmd`
- "Monetary Policy and Labor Earnings" → `monetary-policy-heterogeneity.qmd`
- "Subjective Beliefs and Market Returns" → `ibes-market-returns.qmd`

### Step 2: Create the Landing Page File

Create a new `.qmd` file in the `/papers/` directory with your chosen filename.

**Location:** `/papers/[your-slug].qmd`

### Step 3: Copy and Adapt the Template

Use this template, replacing ALL_CAPS placeholders with actual information:

```yaml
---
title: "FULL PAPER TITLE"
author: 
  - name: FIRST AUTHOR NAME
    affiliation: FIRST AUTHOR INSTITUTION
  - name: SECOND AUTHOR NAME
    affiliation: SECOND AUTHOR INSTITUTION
  # Add more authors as needed
date: "YYYY"
abstract: |
  WRITE YOUR ABSTRACT HERE. Can span multiple lines.
  Just maintain the indentation.

# Google Scholar metadata - CRITICAL for indexing
format:
  html:
    include-in-header:
      text: |
        <meta name="citation_title" content="FULL PAPER TITLE">
        <meta name="citation_author" content="LASTNAME, FIRSTNAME">
        <meta name="citation_author" content="LASTNAME2, FIRSTNAME2">
        <!-- Add one citation_author line per author -->
        <meta name="citation_publication_date" content="YYYY">
        <meta name="citation_pdf_url" content="https://felipeiachan.github.io/working_papers/ACTUAL_PDF_FILENAME.pdf">

page-layout: article
toc: false
---

## Abstract

COPY YOUR ABSTRACT HERE (same as above, for display).

[Download PDF](../working_papers/ACTUAL_PDF_FILENAME.pdf){.btn-download}

## Status

**STATUS HERE**, *Journal Name if Applicable*

## Authors

- **FIRST AUTHOR NAME** (Institution)
- **SECOND AUTHOR NAME** (Institution)
<!-- Add more as needed -->
```

### Step 4: Fill in the Metadata Carefully

#### Critical Fields for Google Scholar:

1. **citation_title**: Exact paper title (same as `title:` field)
2. **citation_author**: One line per author in format "Lastname, Firstname"
   - Order matters! List in paper authorship order
   - Example: `<meta name="citation_author" content="Iachan, Felipe S.">`
3. **citation_publication_date**: Use YYYY format for working papers
4. **citation_pdf_url**: Full URL to the PDF on your deployed site
   - Replace `felipeiachan.github.io` with your actual domain
   - Must match the actual PDF filename in `/working_papers/`

#### PDF Link:

The download button link should use **relative path**: `../working_papers/FILENAME.pdf`

This works because:
- Landing page is at `/papers/slug.qmd`
- PDF is at `/working_papers/filename.pdf`
- `..` goes up one level from `/papers/` to root

### Step 5: Update the Working Papers Index

Edit `/working-papers.qmd` to add a link to your new landing page:

**Format:**
```markdown
"Paper Title", joint with Coauthor Names. *Status Information*. [[page](papers/your-slug.qmd), [pdf](working_papers/FILENAME.pdf)]
```

**Example:**
```markdown
"Minimum wages, Inequality, and the Informal Sector", joint with Luiz Brotherhood and Rafael Machado Parente. *Revised and resubmitted, American Economic Review*. [[page](papers/minwage-inequality.qmd), [pdf](working_papers/Minw_Ineq_Inf.pdf)]
```

### Step 6: Test the Page

1. Run `quarto render` or preview the site
2. Navigate to the working papers page
3. Click the `[page]` link - should open the landing page
4. Click the download button - should download the PDF
5. View page source (browser: right-click → View Page Source)
6. Search for `citation_` - verify all meta tags are present

## Complete Example

Prefer using the existing working pages in this repo as the canonical examples:
- `/papers/minwage-inequality.qmd`
- `/papers/ibes-market-returns.qmd`
- `/papers/monetary-policy-heterogeneity.qmd`

The template in this document is intentionally minimal; the live examples above are guaranteed to stay aligned with the site’s current conventions.

## Common Issues and Troubleshooting

### Issue: PDF Link Broken (404 Error)

**Problem:** Clicked download button but PDF doesn't load.

**Solutions:**
1. Check the PDF exists in `/working_papers/` directory
2. Verify filename matches exactly (case-sensitive!)
3. Check relative path: from `/papers/` you need `../working_papers/file.pdf`

### Issue: Google Scholar Not Indexing

**Problem:** Paper doesn't appear in Google Scholar after weeks.

**Checklist:**
- [ ] Are `citation_` meta tags in the HTML source? (View page source)
- [ ] Is `citation_pdf_url` a direct link to PDF (not a landing page)?
- [ ] Is the PDF publicly accessible without login?
- [ ] Is `citation_publication_date` in YYYY or YYYY/MM format?
- [ ] Did you submit the site to Google Scholar (optional but helps)?

### Issue: Authors Not Displaying Correctly

**Problem:** Author names look wrong in Scholar or on page.

**Solutions:**
1. In `citation_author`, use format: "Lastname, Firstname Middlename"
2. In page `author:` section, use natural order: "Firstname Lastname"
3. Each author needs their own `citation_author` meta tag

## Quick Reference

### Required Files and Locations

```
website/
├── papers/
│   ├── minwage-inequality.qmd          # Landing page
│   ├── ibes-market-returns.qmd         # Landing page
│   └── monetary-policy-heterogeneity.qmd  # Landing page
├── working_papers/
│   ├── Minw_Ineq_Inf.pdf              # Actual PDF
│   ├── IBES_and_Market_Returns.pdf    # Actual PDF
│   └── Monetary_Policy_and_Heterogeneity.pdf  # Actual PDF
└── working-papers.qmd                  # Index page with links
```

### Meta Tag Reference

**Required meta tags for Google Scholar:**
```html
<meta name="citation_title" content="Paper Title">
<meta name="citation_author" content="Lastname, Firstname">
<meta name="citation_publication_date" content="YYYY">
<meta name="citation_pdf_url" content="https://domain.com/path/to/file.pdf">
```

**Optional but recommended:**
```html
<meta name="citation_abstract" content="Abstract text...">
<meta name="citation_keywords" content="keyword1; keyword2; keyword3">
```

## For AI Agents

When asked to "add a working paper" or "create a landing page for [paper]":

1. **Ask for missing information** if not provided:
   - PDF filename (in `/working_papers/`)
   - Full author list with affiliations
   - Abstract or brief description
   - Current status (R&R, under review, working paper, etc.)

2. **Create the landing page** in `/papers/[slug].qmd` using the template

3. **Update the index** in `/working-papers.qmd` with both [page] and [pdf] links

4. **Verify** by checking:
   - File paths are correct
   - All authors listed
   - Meta tags properly formatted
   - Links use correct relative paths

5. **Test if possible**: Preview the site and click through to verify

## Additional Resources

- **Google Scholar Guidelines**: https://scholar.google.com/intl/en/scholar/inclusion.html
- **Quarto Documentation**: https://quarto.org/docs/websites/
- **This site's template**: See `/papers/minwage-template.qmd` (older template, may be outdated)

---

**Last Updated:** January 2, 2026  
**Maintainer:** Felipe S. Iachan

