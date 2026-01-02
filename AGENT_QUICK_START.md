# Quick Start for AI Agents: Adding Working Papers

## TL;DR

To add a working paper landing page:

1. **Get info**: title, authors, affiliations, PDF filename, status, year
2. **Create**: `/papers/[slug].qmd` using template below
3. **Update**: Add entry to `/working-papers.qmd`
4. **Verify**: PDF link works, meta tags present in HTML source

## Minimal Template

```yaml
---
title: "PAPER TITLE"
author: 
  - name: AUTHOR NAME
    affiliation: INSTITUTION
date: "YYYY"
abstract: |
  ABSTRACT TEXT HERE

format:
  html:
    include-in-header:
      text: |
        <meta name="citation_title" content="PAPER TITLE">
        <meta name="citation_author" content="LASTNAME, FIRSTNAME">
        <meta name="citation_publication_date" content="YYYY">
        <meta name="citation_pdf_url" content="https://felipeiachan.github.io/working_papers/FILE.pdf">

page-layout: article
toc: false
---

## Abstract

ABSTRACT TEXT HERE

[Download PDF](../working_papers/FILE.pdf){.btn-download}

## Status

**STATUS**, *Journal (if applicable)*

## Authors

- **AUTHOR NAME** (Institution)
```

## Working Papers Index Entry

Add to `/working-papers.qmd`:

```markdown
"Paper Title", joint with Coauthors. *Status*. [[page](papers/slug.qmd), [pdf](working_papers/FILE.pdf)]
```

## Critical Points

1. **citation_pdf_url**: Must be full URL with actual deployed domain
2. **PDF relative path**: Use `../working_papers/file.pdf` from landing page
3. **citation_author**: Format as "Lastname, Firstname" (one per author)
4. **Slug**: lowercase-with-hyphens, descriptive but short
5. **Repo convention**: working paper PDFs go in `/working_papers/`; landing pages go in `/papers/`; the index is `working-papers.qmd`

## See Also

- Full documentation: `WORKING_PAPER_INSTRUCTIONS.md`
- Current examples: `/papers/minwage-inequality.qmd`, `/papers/ibes-market-returns.qmd`

