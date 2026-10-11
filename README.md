# Barnebeck.github.io

Academic website of Thomas Barnebeck Andersen, built with [Hugo Blox](https://hugoblox.com) (Academic CV template) and deployed to GitHub Pages by `.github/workflows/publish.yaml`.

## Editing
- Profile, affiliation, links, education: `content/authors/admin/_index.md` (photo: `avatar.jpg` in the same folder)
- Home page layout: `content/_index.md`
- Publications: one folder per paper in `content/publication/` (copy an existing `index.md` and edit)
- Commentary / Teaching / Vitae: `content/commentary.md`, `content/teaching.md`, `content/vitae.md`
- CV PDF: put it at `static/uploads/cv.pdf`

## Local preview
`hugo server` (needs Hugo extended 0.135.0 and Go), then open http://localhost:1313
