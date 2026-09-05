# Course Website Template

A Jekyll-based course website template designed for reuse across semesters.
Hosted on GitHub Pages.

## Structure

```
course-site/
├── _config.yml          ← Edit this for each new course
├── _data/
│   ├── schedule.yml     ← Weekly schedule — edit rows here
│   ├── announcements.yml← Add new entries at the top
│   ├── assignments.yml  ← Assignment descriptions and due dates
│   └── resources.yml    ← Grouped resource links
├── _layouts/
│   └── default.html     ← Shared layout — rarely needs editing
├── assets/css/
│   └── main.css         ← Design system — edit for rebrand
├── index.html           ← Home page (announcements + schedule)
└── pages/
    ├── syllabus.html
    ├── assignments.html
    ├── project.html
    └── resources.html
```

## How to update content

**Add an announcement:** open `_data/announcements.yml`, add a new entry
at the top (newest first). Format:
```yaml
- date: "Oct 5"
  text: "Assignment 1 is now available."
```

**Update the schedule:** open `_data/schedule.yml`. Each row is one week.
Add slides or lab URLs to the `slides_url` and `lab_url` fields —
they appear as links automatically when non-empty.

**Add an assignment:** open `_data/assignments.yml`. Add a new entry,
set `url` to the assignment link when it is released.

**Add a resource:** open `_data/resources.yml`. Add to an existing
category or create a new one.

## Reusing for a new course

1. Duplicate this repository (or copy it to a new repo)
2. Edit `_config.yml` — change course code, name, semester, instructor
3. Clear `_data/announcements.yml` and replace with your first announcement
4. Replace `_data/schedule.yml` with your new schedule
5. Replace `_data/assignments.yml` and `_data/resources.yml`
6. Update the prose content in each page under `pages/`
7. Push to GitHub — GitHub Pages builds automatically

## Local development

```bash
gem install bundler jekyll
bundle init
bundle add jekyll
bundle exec jekyll serve
```

Visit `http://localhost:4000` to preview.

## Hosting on GitHub Pages

1. Push to a GitHub repository
2. Go to Settings → Pages → Source: Deploy from branch → main → / (root)
3. Your site appears at `https://yourusername.github.io/repo-name/`

To host under your personal site (e.g. `yoursite.com/cs5xxx/`):
set `baseurl: "/cs5xxx"` in `_config.yml` and push to a subfolder repo.
