# Barnebeck.github.io

Academic website of Thomas Barnebeck Andersen, built with [Hugo Blox](https://hugoblox.com) (Bootstrap edition, the successor of the classic "Academic" theme) and deployed to GitHub Pages by `.github/workflows/publish.yaml`.

## Editing
- Profile, affiliation, links, education: `content/authors/admin/_index.md` (photo: `avatar.jpg` in the same folder)
- Home page sections (about, recent work, commentary, teaching, contact): `content/_index.md`
- Publications: one folder per paper in `content/publication/` (copy an existing `index.md` and edit)
- Full commentary list / CV page: `content/commentary.md`, `content/vitae.md`
- Colours and fonts: `data/themes/academic_blue.toml`, `data/fonts/academic.toml`, small CSS tweaks in `assets/scss/custom.scss`
- `layouts/partials/{analytics,components}/` hold two tiny overrides that keep the theme building on Hugo ≥ 0.134
- CV PDF: put it at `static/uploads/cv.pdf`

## Local preview
`hugo server` (needs Hugo extended 0.135.0 and Go), then open http://localhost:1313
