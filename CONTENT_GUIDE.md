# Content Guide (internal — not shown on the live site)

This file is just a reference for editing your own site. It lives in the repo but nothing links to it from any page, so visitors to your website will never see it. You can only find it by browsing the repo itself on github.com.

General rule: everything you edit lives in `content/*.json`. Images go in `assets/images/`. Always upload an image first, then reference its path in the JSON.

---

## Add a News item
File: `content/news.json`

```json
{
  "date": "2026-08",
  "text": "What happened.",
  "image": "assets/images/your-file.jpg",
  "gif": "",
  "url": "https://example.com",
  "url_label": "Link text"
}
```
- `date`: `"YYYY-MM"` or `"YYYY-MM-DD"`. Order in the file doesn't matter, it auto-sorts newest first.
- `image` / `gif`: optional. Use one or the other, not both. Leave `""` if none.
- `url` / `url_label`: optional. Makes the entry clickable. Omit both if there's no link.

---

## Add a Project
File: `content/projects.json`

```json
{
  "id": "unique-short-id",
  "title": "Project Title",
  "summary": "1-3 sentence description.",
  "image": "assets/images/your-file.jpg",
  "image_alt": "Short description of the image for accessibility",
  "url": "pages/publications.html"
}
```
- `id`: must be unique across all projects, lowercase, hyphens instead of spaces.
- `url`: can point to an external link (`https://...`), another page on your own site (`pages/cv.html`), or a dedicated long-form project page if you build one under `pages/projects/`.

---

## Add a Publication
File: `content/publications.json`

```json
{
  "id": "unique-short-id",
  "title": "Full Title of the Paper",
  "content": "Author, A., Author, B.",
  "link": "https://doi.org/xxxx",
  "publisher": "Journal Name, Year",
  "image": "assets/images/publications/your-file.jpg",
  "tags": ["journal"],
  "buttons": [],
  "created_at": 1735689600,
  "updated_at": 1735689600
}
```
- `link`: leave `""` if you don't have a DOI/URL yet.
- `tags`: pick from `content/publications_tags.json` (currently: `key_publications`, `journal`, `book_chapter`, `manuscript`, `conference`, `preprint`). Add a new tag there first if you need a new category.
- `created_at` / `updated_at`: Unix timestamps, controls sort order. Easiest way to get one: search "epoch converter" online, pick a date, copy the number.

---

## Add a CV entry
Files: `content/cv.json` (short/summary version) or `content/cv_full.json` (complete version)

```json
{
  "title": "Role or Award Title",
  "organization": "Institution or Organization",
  "dates": "Month Year - Month Year",
  "logo": "assets/images/institution-placeholder.svg",
  "logo_alt": "Organization name logo",
  "flag": "US",
  "flag_alt": "United States flag",
  "bullets": [
    "First detail.",
    "Second detail."
  ]
}
```
- Add this inside the `"entries"` array of the right section (e.g. "Honors and Awards", "Professional Memberships"). To add a whole new section, copy this pattern:
```json
{
  "title": "New Section Title",
  "entries": [ /* entries go here */ ]
}
```
- `logo`: optional but recommended you keep the placeholder path if you don't have a real logo, don't delete the field.
- `flag`: optional, two-letter country code (`US`, `NG`, etc.). Omit both `flag` and `flag_alt` if not needed.
- `bullets`: optional, omit the field entirely if there are none.

---

## Add a link to the Elsewhere page
File: `pages/elsewhere.html` (this one is a plain HTML page, not JSON)

Find the right `<section class="cv-section">` for the category (or add a new section following the same pattern), then add a line inside its `<ul class="cv-list">`:

```html
<li><a href="https://example.com" target="_blank" rel="noopener">Platform Name</a></li>
```

---

## Update your homepage bio, contact, or social links
File: `content/site.json`
- `bio_html`: your homepage bio paragraph. Can include basic HTML tags like `<br>` for line breaks. Replace or expand this paragraph as needed in <code>content/site.json</code>.
- `contact`: array of plain text lines (email, department, etc.)
- `social_links`: array of `{ "label": "...", "url": "...", "icon": "fa-brands fa-xxxx" }`. Icon names come from Font Awesome (fontawesome.com/icons), search there for the right one.

---

## General checklist before committing
1. Upload any new image to `assets/images/` first, note its exact filename.
2. Edit the relevant JSON file, add your entry using the templates above.
3. Double check commas: every entry except the last one in a list needs a comma after its closing `}`.
4. Paste your edited content into a JSON validator (e.g. jsonlint.com) if unsure, a single missing comma or bracket will break the whole file.
5. Commit.
