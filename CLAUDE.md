# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Personal academic website for Rocco Zizzamia (University of Oxford), built on the [Academic Pages](https://academicpages.github.io/) Jekyll template (Minimal Mistakes theme). Hosted on GitHub Pages at `roccozizzamia.github.io`.

## Deployment

Push to `master` → GitHub Pages auto-builds and deploys. There is no CI/CD config or GitHub Actions — GitHub Pages runs Jekyll natively. The `_site/` directory is the build output (gitignored in practice but present locally after a build).

## Build & Serve Locally

```bash
bundle install                # install Ruby dependencies (first time / after Gemfile changes)
jekyll serve -l -H localhost  # serve at localhost:4000 with live reload
```

Prerequisites: Ruby, Bundler, Node.js. On macOS: `brew install ruby node && gem install bundler`.

If `bundle install` fails, delete `Gemfile.lock` and retry.

**Important:** `_config.yml` changes require restarting the server — live reload does not pick them up.

## JS Build

```bash
npm run build:js   # uglify and concatenate JS into assets/js/main.min.js
```

Only needed if modifying JS plugins or `assets/js/_main.js`. Rarely touched.

## Site Architecture

### Where content lives

The site uses Jekyll collections, but **all content pages are hand-written in `_pages/`** — not auto-generated:

| File | URL | Layout |
|------|-----|--------|
| `_pages/about.md` | `/` (homepage) | `single` |
| `_pages/publications.md` | `/publications/` | `archive` |
| `_pages/workinprogress.md` | `/workinprogress/` | `archive` |
| `_pages/otherwriting.md` | `/otherwriting/` | `archive` |
| `_pages/cv.md` | `/cv/` | `archive` |

Navigation order is set in `_data/navigation.yml`.

### Configuration

- **`_config.yml`** — Site metadata, author sidebar info, social links, collection definitions, publication categories
- **`_data/navigation.yml`** — Header nav links and order
- **`_includes/author-profile.html`** — Sidebar (photo, bio, links). Reads from `author:` block in `_config.yml`
- **`_sass/_variables.scss`** — Theme customization

### Static files

- `files/` — PDFs, replication packages, survey instruments, CV. Referenced as `/files/filename.ext`
- `images/` — Site images including author avatar (`RZphoto.jpg`)

### Unused template artifacts

`_publications/`, `_teaching/`, `_talks/`, `_portfolio/`, `_posts/`, and `markdown_generator/` are from the upstream Academic Pages template. The site doesn't actively use them — all content is in `_pages/`.

## Content Patterns

### Adding a publication or working paper

Entries are written as raw HTML/Markdown directly in `_pages/publications.md` or `_pages/workinprogress.md`. The consistent pattern is:

```markdown
[**Paper Title**](https://doi-or-url) \
with Coauthor Name \
*Journal Name,* Year (Vol. X, Issue Y) \
<small>[[Draft](/files/draft.pdf) | [Code](/files/code.zip) | [Op-Ed](https://url)]</small>
<details>
  <summary>Abstract</summary>
Abstract text here.
</details>
<p> </p>

<br>
```

Key details:
- `<details>` / `<summary>` for expandable abstracts (publications page uses "Abstract", work-in-progress uses "Details")
- Supplementary links wrapped in `<small>` tags with `[[Label](url)]` format
- `<p> </p>` and `<br>` for spacing between entries
- External links use `{:target="_blank"}` kramdown attribute (homepage/about page), but publication pages use raw HTML links
- File downloads link to `/files/` directory

### Other writing page

Simpler format — just linked titles with coauthors and publication venue, no abstracts/details blocks.

### CV page

Links to a PDF at `/_pages/rocco-zizzamia-cv.pdf`. To update the CV, replace that PDF file.
