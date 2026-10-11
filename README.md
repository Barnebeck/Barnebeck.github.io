# barnebeck.github.io

Academic website of Thomas Barnebeck Andersen, Professor of Economics, University of Southern Denmark.
Live at <https://barnebeck.github.io>.

Built with [Hugo](https://gohugo.io) and the maintained **Hugo Blox Kit** theme (`github.com/HugoBlox/kit/modules/blox`,
Tailwind CSS v4), deployed to GitHub Pages by GitHub Actions. Light and dark mode follow the visitor's system
setting; the sun/moon button in the header lets visitors override it.

## Where things live

| What you want to change | File |
| --- | --- |
| Name, role, photo, short bio, links, research interests, education | `data/authors/me.yaml` (photo: `assets/media/authors/me.jpg`) |
| Home page sections (About, Recent publications, Commentary, Teaching, Contact) | `content/_index.md` |
| Publications (one folder per item) | `content/publications/<year>-<short-title>/` |
| Research page intro text | `content/publications/_index.md` |
| Full commentary list | `content/commentary.md` |
| Vitae | `content/vitae.md` |
| Navigation menu | `config/_default/menus.yaml` |
| Site title, colours, fonts, dark mode, footer | `config/_default/params.yaml` |

Text is Markdown. In YAML, keep the indentation exactly as it is (spaces, not tabs).

## Adding a publication

1. Copy an existing folder in `content/publications/`, e.g. `2024-hysteresis-and-the-long-shadow-of-the-exchange-rate-r`,
   and rename it `<year>-<short-title>`.
2. Edit `index.md`:
   ```yaml
   title: "Paper title"          # write it exactly as published; a trailing "?" is fine
   authors:
     - me                         # "me" = Thomas (links to data/authors/me.yaml)
     - "Co-author Name"
   date: "2026-01-01"             # only the year is shown
   publication_types: ["article-journal"]   # article-journal | chapter | article (book review) | report
   publication:
     name: "Journal Name"         # for a chapter: the book title
     volume: "12"                 # optional
     issue: "3"                   # optional
     pages: "100–120"             # optional
     publisher: "..."             # chapters only (optional)
     editor: "..."                # chapters only (optional)
   publication_note: "Book review"   # book reviews only
   abstract: "..."                # optional; shown on the paper's page
   hugoblox:
     ids:
       doi: "10.xxxx/xxxxx"       # creates the DOI button
   links:
     - type: source               # shown as "Article"
       url: "https://..."
     - type: pdf                  # optional
       url: "https://..."
   ```
3. Edit `cite.bib` in the same folder (this file powers the **Cite** button and the BibTeX box on the
   paper's page). Tip: `curl -LH "Accept: application/x-bibtex" https://doi.org/<DOI>` prints a publisher
   BibTeX record you can paste in.

The Research page groups items automatically: *Journal articles* (`article-journal`, `report`),
*Book chapters* (`chapter`) and *Book reviews* (`article`), newest first. The home page shows the 8 most
recent journal articles (change `count` in `content/_index.md`).

Each publication page also carries Google Scholar `citation_*` meta tags (title, authors, year, journal or book,
volume, issue, pages, DOI, PDF), generated from the fields above.

Abstracts were taken from publisher metadata (Crossref, or OpenAlex where Crossref had none); the source is noted
in each file as `abstract_source`. Papers without an abstract simply show none.

## Preview locally

Requirements: Hugo **extended** 0.162.0 (version pinned in `hugoblox.yaml`), Go, Node.js 22+ and pnpm.

```bash
pnpm install            # installs Tailwind CSS (needed by Hugo)
hugo server             # open http://localhost:1313
```

## Publishing

Pushing to `master` runs `.github/workflows/deploy.yml` (which calls `build.yml`) and publishes the site.
Repository Settings → Pages → Source must be **GitHub Actions**. Pull requests to `master` are built but not
deployed, which is a convenient way to check a change.

## Local customisations (keep in mind when upgrading the theme)

The look is the theme's, with a few small, self-contained additions:

- `layouts/_partials/hbx/blocks/tba-profile/`, `tba-section/`, `tba-publications/`: plain home-page blocks
  (profile, text section, recent publications).
- `layouts/_partials/tba/`: publication entry, authors, venue line and grouping.
- `layouts/publications/section.html` and `page.html`: Research page and individual paper pages.
- `layouts/_partials/hooks/head-end/scholar-meta.html`: Google Scholar meta tags.
- `layouts/_partials/functions/build_links.html`: copy of the theme file with a one-line fix
  (`$seen.Set "set" (dict "_init" true)`), needed because the current theme version crashes with Hugo 0.162
  when a page has links. After a theme upgrade, delete this file and run `hugo`; if it builds, the fix is no
  longer needed.
- `assets/css/hbx/blocks/shared/tba/site.css`: typography, spacing and list styling.
- `i18n/en.yaml`: button labels ("Article" instead of "Source Document").

Old addresses from the previous site (`/publication/...`) redirect to the new ones (`aliases:` in each file).

## Upgrading the theme

```bash
hugo mod get -u github.com/HugoBlox/kit/modules/blox
hugo mod tidy
hugo            # check the build, then preview with hugo server
```

If a new theme version requires a newer Hugo, update `build.hugo_version` in `hugoblox.yaml`.
