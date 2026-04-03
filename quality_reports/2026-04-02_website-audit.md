# Website Audit Report

**Date:** 2026-04-02

---

## ERRORS (will break things for visitors)

### 1. `chrome-extension://` links — broken for all visitors
- `_pages/publications.md:27` — Wave 1 working paper link starts with `chrome-extension://efaidnbmnnnibpcajpcglclefindmkaj/https://cramsurvey.org/...`
- `_pages/publications.md:28` — Wave 2 working paper link, same issue
- `_pages/publications.md:29` — Wave 3 working paper link, same issue
- `_pages/publications.md:80` — Policy report link for "Locked down and locked out", same issue
- **Fix:** Strip the `chrome-extension://efaidnbmnnnibpcajpcglclefindmkaj/` prefix from all four URLs. These were copied from an Adobe Acrobat browser extension and only work on your machine.

### 2. Missing file: `CREST_BL.pdf`
- `_pages/workinprogress.md:40` links to `/files/CREST_BL.pdf` — this file does not exist in `files/`
- **Fix:** Add the file, or remove the link

### 3. Working paper link missing `https://`
- `_pages/workinprogress.md:59` — `[Working Paper](www.theigc.org/sites/default/files/2025-03/Nawaz-et-al-working-paper-march-2025.pdf)` — this renders as a relative link (pointing to your own domain) because it lacks a protocol
- **Fix:** Change to `https://www.theigc.org/...`

### 4. Inconsistent Code link path
- `_pages/publications.md:13` — `[Code](/_pages/_assets/dofiles.zip)` uses the `/_pages/_assets/` path, while all other file links use `/files/`. The file exists in both locations, but `/_pages/_assets/` is non-standard and may not be served by Jekyll depending on config
- **Fix:** Change to `/files/dofiles.zip` for consistency

---

## INCONSISTENCIES

### 5. Title mismatch: page title vs nav label
- `_pages/publications.md:2` — front matter `title: "Research"` but nav says "Publications"
- The page heading is "Research" but the header nav link says "Publications". Visitors click "Publications" and land on a page titled "Research"
- **Fix:** Align the title (your call which name to use)

### 6. "Forthcoming" status may be outdated
- `_pages/publications.md:12` — "Journal of Behavioral and Experimental Economics (Forthcoming)" — if this has been published, update with volume/issue/year. Worth checking periodically.

### 7. Typo: "VovDev" → "VoxDev"
- `_pages/otherwriting.md:10` — `*VovDev*, 28 Oct. 2025` should be `*VoxDev*`

### 8. Typo: "Philippenes" → "Philippines"
- `_pages/workinprogress.md:26` — `[Philippenes](https://www.socialscienceregistry.org/trials/4658)`

### 9. Typo: "multifacteted" → "multifaceted"
- `_pages/workinprogress.md:51` — in the details text for the climate change paper

### 10. Typo: "anticiptory" → "anticipatory"
- `_pages/workinprogress.md:73` — in the portfolio theory paper details

### 11. Typo: "f ield" → "field"
- `_pages/workinprogress.md:29` — stray space in "f ield agents"

### 12. Summary label inconsistency
- Publications page uses `<summary>Abstract</summary>` for most entries but `<summary>Details</summary>` for the first entry (Ignorance is bliss)
- Work-in-progress page consistently uses `<summary>Details</summary>`
- **Suggestion:** Use "Abstract" on the publications page and "Details" on work-in-progress, consistently

---

## STALE / DEAD WEIGHT

### 13. Legacy `.markdown` files are still in `_pages/`
- `_pages/02_research.markdown` — old version of the publications page (fewer publications, different format, different permalink `/research/`). It's accessible at `/research/` and contains outdated content
- `_pages/03_workinprogress.markdown` — old version of work-in-progress page (numbered items, completely different project list). Shares permalink `/workinprogress/` with the current `workinprogress.md`, which means **one will shadow the other** depending on Jekyll's resolution order
- **Fix:** Delete both files. The `.md` versions are the current ones. Having two files with the same permalink (`/workinprogress/`) is a build conflict.

### 14. Duplicate files in `_pages/_assets/` and `files/`
- Every file in `_pages/_assets/` is duplicated in `files/`. Only `files/` is linked to (except the one error in #4). The `_pages/_assets/` directory appears to be a staging area that was never cleaned up.
- **Fix:** Consider deleting `_pages/_assets/` entirely once you've confirmed `files/` has everything

### 15. Timezone set to `America/Los_Angeles`
- `_config.yml:293` — You're at Oxford. Likely inherited from the template.
- **Fix:** Change to `Europe/London` (cosmetic, affects post timestamps)

---

## SUGGESTIONS

### 16. The "Group vs Individual Coaching" paper: conditional accept vs. published
- `_pages/workinprogress.md:23` — Shows "Conditional Accept, American Economic Review: Insights". If this has been accepted/published, it should move to publications.md. If still conditional accept, the status is fine, but worth checking.

### 17. CV link uses unusual path
- `_pages/cv.md:9` — links to `/_pages/rocco-zizzamia-cv.pdf`. The file exists there and also at `files/rocco-zizzamia-cv.pdf`. Using `/files/rocco-zizzamia-cv.pdf` would be more consistent with the rest of the site.

### 18. No `<meta>` description set
- `_config.yml:14` — `description` is commented out. Search engines and social previews will show no description for your site.
- **Fix:** Uncomment and add a brief academic bio/description
