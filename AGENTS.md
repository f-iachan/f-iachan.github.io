# Agent Guidance (Quarto Academic Site)

## Roles & Responsibilities

### 1) Site Architect
- Implement new site map:
  - Create: working-papers.qmd, publications.qmd, contact.qmd
  - Update navbar in _quarto.yml
- Ensure consistent routing and internal links.

Deliverables:
- Updated _quarto.yml
- New pages with placeholder content and correct sections

### 2) Working Paper Indexer (Scholar)
- For each working paper:
  - Create a landing page in /papers/<slug>.qmd (or /working-papers/<slug>.qmd if we restructure)
  - Add citation meta tags:
    - citation_title
    - citation_author (repeat per author)
    - citation_publication_date (YYYY/MM or YYYY)
    - citation_pdf_url (direct)
  - Ensure PDF is in repo and linked stably

Deliverables:
- At least 1 working-paper landing page end-to-end as a template
- Working Papers index page lists each WP with [Page] [PDF]

Verification:
- View page source includes correct meta tags
- PDF opens directly without redirects/login

### 3) Publications Curator
- Create publications list separate from working papers.
- Prefer a bibliography file (BibTeX) if available; otherwise start manual and later migrate to BibTeX.
- Organize as:
  - Peer-reviewed
  - Accepted / Forthcoming
  - Policy / Other (optional)

Deliverables:
- publications.qmd with clean structure and links

### 4) CV Harmonizer (Lattes-first)
- Prefer Lattes as the canonical factual record when conflicts arise. Prompt user for conflict resolution.
- Update cv.qmd to:
  - Be readable HTML
  - Include “Download PDF” link
  - Include last-updated date
- If cv-pdf.qmd exists, ensure it compiles; otherwise keep HTML CV as priority.

Deliverables:
- cv.qmd updated
- (Optional) cv-pdf.qmd updated and renderable

### 5) Identity & Discoverability Agent
- Implement identity.qmd:
  - Google Scholar link
  - Lattes link
  - ORCID link
  - RePEc/IDEAS link (if exists)
  - SSRN link (if exists)
  - GitHub link
  - Optional: email, affiliation, short disambiguation line
- Add schema-like clarity in prose (not heavy markup).

Deliverables:
- identity.qmd live and linked in navbar

### 6) Analytics & Migration Agent
- Add GA4 Measurement ID via _quarto.yml config.
- If old Google Sites used GA, reuse the same GA4 property if desired (to keep continuity).
- Add a short “site moved” notice on Google Sites (manual step) pointing to new domain.

Deliverables:
- Analytics configured in Quarto
- Short migration note text

## Implementation conventions
- Keep working paper PDFs under /papers/ (stable).
- Prefer simple Markdown, avoid JS dependencies.
- Minimal CSS changes: only in custom.scss.

## Final checklist
- quarto render works
- sitemap exists after deploy
- Working Papers pages have citation meta tags
- Identity page has all external links
- Navbar updated and consistent
