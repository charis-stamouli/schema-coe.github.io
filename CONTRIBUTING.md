# Contributing to the SCHEMA website

This page explains how members of the SCHEMA Center of Excellence keep the website up to date. Everything is plain text (BibTeX, Markdown, YAML) — no web design needed.

Four things you might edit:

1. [Your publications](#1-publications) — `_bibliography/pi/<name>.bib`
2. [Your profile](#2-your-profile-people) — `_people/<your-name>.md`
3. [News](#3-news) — `_data/news.yml`
4. [How to submit changes](#4-submitting-changes-important) — **always via a pull request reviewed by the Zardini team**

---

## 1. Publications

Each PI owns **one** bibliography file: `_bibliography/pi/<name>.bib` (e.g. `zardini.bib`). Only edit your own file. On every build, all PI files are merged automatically into the full publication list — you never touch the combined list.

Add entries in standard BibTeX. A typical entry:

```bibtex
@inproceedings{MatniScalable2026,
  author    = {Matni, Nikolai and Coauthor, Alex},
  title     = {A Great SCHEMA Paper},
  booktitle = {Proc. of the Conference on Decision and Control},
  year      = {2026},
  url       = {https://arxiv.org/abs/2601.12345},
  abstract  = {We show that ...}
}
```

Two fields matter for how the entry displays — please include both:

- **`url`** — makes the paper **title clickable** on the site. Point it at the arXiv/DOI/publisher page. Without it, the title is not a link.
- **`abstract`** — required for the **"Abstract" toggle** to appear under the entry. If there is no abstract field, the abstract button won't show.

Every entry also gets an automatic **"BibTeX"** toggle, so people can copy the citation.

### Optional: attach media and press

You can add a talk video, slides, and press coverage. Each needs a `*_show` flag set to `true` **and** the matching link field:

```bibtex
  video_show  = {true},
  video       = {https://youtu.be/XXXXXXXX},
  slides_show = {true},
  slides      = {https://.../slides.pdf},
  press_show  = {true},
  press       = {https://news.mit.edu/...}
```

This adds **Talk**, **Slides**, and **Press** links to the entry. Other media (datasets, code, custom badges) can be added on request — open an issue or ask the Zardini team.

### Entry types and status flags

- Use the right type so it lands in the right section: `@unpublished` (Preprints), `@book`, `@article` / `@inproceedings` / `@incollection` / `@techreport` (Publications), `@misc` (Workshop Papers), `@patent`, `@report`, `@phdthesis` / `@thesis`.
- Status keywords (optional): `keywords = {sub}` (submitted — shown as a preprint / kept out of the main list), `keywords = {press}` (in press), `keywords = {prep}` (in preparation).
- **Keys must be unique** across all PI files (e.g. prefix with your last name). Do not delete other people's entries — the build checks for this.

---

## 2. Your profile (People)

Everyone has a file in `_people/`, e.g. `_people/gioele-zardini.md`. Edit it to update your bio, photo, and links. The top block (between the `---` lines) is settings; the text below it is your bio (Markdown).

```markdown
---
layout: person
title:  "Your Name"
last:   "Lastname"          # used for alphabetical sorting
position: student            # pi | afosr | postdoc | student | alumni
institution: "Your University"
role: "PhD Student (EECS)"   # optional, shown for students
img: YourPhoto.jpg           # file goes in img/people/
email: you@university.edu
website: https://your-site
github: yourhandle
linkedin: yourhandle
gscholar: XXXXXXXXXXXX       # the id from your Scholar profile URL
twitter: yourhandle
---

Your short bio goes here. Keep it to a few sentences.
```

Notes:

- **Photo:** add the image to `img/people/` and set `img:` to the filename. Square images look best.
- **Only the fields you fill in appear** — leave out what you don't want to show (e.g. omit `twitter` and no Twitter icon shows).
- **Positions** control which section you appear in: `pi`, `afosr`, `postdoc`, `student`, `alumni`. The Lead PI is the `pi` entry with `lead: true`.
- **Alumni:** set `wherefrom:` (your former role) and `current:` (where you are now).

---

## 3. News

News items live in `_data/news.yml`, grouped by year, newest shown first. To add an item, add a line under the right year:

```yaml
- year: 2026
  events:
    - date: "09/2026"
      description: "SCHEMA kicked off at XXX! Read more <b><a class='black-link' href='https://...'>here</a></b>."
```

- `date` is a free-text string (e.g. `"09/2026"` or `"09/15/2026"`).
- `description` may contain HTML — use `<b>...</b>` and `<a href='...'>...</a>` for links.
- To start a new year, add a new `- year:` block with its own `events:` list.

News appears automatically on both the home page and the News page.

---

## 4. Submitting changes (important)

Please **do not commit directly to `main`.** For every change:

1. **Create a branch** (or your own fork) and commit your edits there.
2. **Push** your branch to GitHub.
3. **Open a pull request** into `main`.
4. **Request a review from someone on the Zardini team** and wait for approval before it is merged.

A couple of automatic checks run on each pull request (the site is built, and the BibTeX files are validated). If a check fails, open the PR's "Checks" tab to see what to fix. When in doubt, ask the Zardini team — we're happy to help.
