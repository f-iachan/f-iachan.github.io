# Felipe S. Iachan - Academic Website

A Quarto-based academic website with FGV brand colors, designed for GitHub Pages hosting.

## Quick Start

### Prerequisites

1. Install [Quarto](https://quarto.org/docs/get-started/)
2. Install a TeX distribution (for PDF CV generation):
   - macOS: `brew install --cask mactex-no-gui`
   - Ubuntu: `sudo apt install texlive-full`
   - Windows: Install MiKTeX

### Local Development

```bash
# Preview the site locally
quarto preview

# Build the site
quarto render
```

### Deployment to GitHub Pages

1. Create a GitHub repository named `felipeiachan.github.io` (or your username)

2. Initialize git and push:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/felipeiachan/felipeiachan.github.io.git
git push -u origin main
```

3. Publish to GitHub Pages:
```bash
quarto publish gh-pages
```

This creates a `gh-pages` branch with the rendered site.

4. In GitHub repository settings → Pages → Source: select `gh-pages` branch.

### Custom Domain (Optional)

1. Purchase domain (e.g., `felipeiachan.com`)
2. Create `CNAME` file in project root with your domain
3. Configure DNS with your registrar:
   - A records pointing to GitHub's IPs
   - Or CNAME record pointing to `felipeiachan.github.io`

See: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

## File Structure

```
website/
├── _quarto.yml          # Main configuration
├── custom.scss          # FGV colors and typography
├── styles.css           # Additional CSS
├── index.qmd            # Home page
├── publications.qmd     # Publications (published papers)
├── working-papers.qmd   # Working papers index (with [page] + [pdf])
├── cv.qmd               # CV (HTML version)
├── cv-pdf.qmd           # CV (PDF source)
├── links.qmd            # Contact + academic profiles (navbar label: Contact)
├── assets/
│   ├── portrait.jpg     # Your photo
│   └── favicon.svg      # Site favicon
├── papers/
│   ├── *.pdf            # Publication PDFs
│   └── *.qmd            # Working paper landing pages (for Scholar indexing)
└── working_papers/
    └── *.pdf            # Working paper PDFs
```

## Customization

### Colors

Edit `custom.scss` to change the color scheme:
```scss
$fgv-blue: #1C2F67;      // Primary color
$fgv-blue-dark: #142452;  // Hover states
```

### Fonts

Current setup uses Source Sans 3 (headings) and Source Serif 4 (body). 
Change in `custom.scss`:
```scss
$font-family-sans-serif: "Your Font", sans-serif;
```

### Adding Publications

Edit `publications.qmd`. Use this format:
```markdown
::: {.publication}
**Paper Title**  
with Coauthor Name  
*Journal Name*, Volume (Year), Pages.  
[[Paper](papers/filename.pdf)] [[Journal](https://doi.org/...)]
:::
```

### Adding Working Papers (for Google Scholar)

For Scholar indexing, create a dedicated page for each working paper:
1. Copy `papers/minwage-template.qmd`
2. Fill in the metadata (especially `citation_*` meta tags)
3. Put the PDF in `working_papers/`
4. Link from `working-papers.qmd`

## Google Scholar Indexing

For Scholar to index your working papers:

1. **PDF requirements:**
   - Host PDFs directly on your site (not just links to SSRN)
   - Include title and authors in the PDF
   - Use standard academic formatting

2. **HTML metadata:**
   - Each paper page needs `<meta name="citation_*">` tags
   - See `papers/minwage-template.qmd` for the template

3. **Site structure:**
   - Have a clear "Research" or "Publications" page
   - Link to paper pages and PDFs from there

4. **Submit to Scholar:**
   - Go to https://scholar.google.com/intl/en/scholar/inclusion.html
   - Request indexing after your site is live

## Updating the CV

1. Edit `cv.qmd` (HTML version) and `cv-pdf.qmd` (PDF version)
2. Rebuild:
```bash
quarto render cv-pdf.qmd  # Generates cv-pdf.pdf
quarto render
```
3. The PDF download link in `cv.qmd` points to `cv-pdf.pdf`

## Troubleshooting

**PDF not generating?**
- Ensure TeX is installed: `quarto check`
- Try: `quarto render cv-pdf.qmd --verbose`

**Fonts not loading?**
- Check browser console for CORS errors
- Google Fonts should work; if using local fonts, ensure they're in `assets/`

**Scholar not indexing?**
- Verify meta tags with View Source
- Check that PDFs are accessible (not behind login)
- Be patient — Scholar crawls infrequently

## License

Content © Felipe S. Iachan. Site template available under MIT License.
