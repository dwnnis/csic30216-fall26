# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Jekyll-based course website template, currently instantiated for a Fall 2026 course
("AI-in-the-Loop in Software Project Cycle AI", CSIC30216, National Yang Ming Chiao Tung University). It's designed
to be duplicated and re-themed for other courses/semesters — the README documents that
reuse workflow in detail.

## Commands

```bash
bundle exec jekyll serve      # local dev server at http://localhost:4000
bundle exec jekyll build      # build to _site/
```

There is no test suite, linter, or CI config in this repo.

## Architecture

All page content is driven by two things: `_config.yml` (site-wide identity/settings)
and the YAML files in `_data/` (structured content). The HTML in `pages/` and
`index.html` is mostly Liquid loops over that data — editing prose directly in those
files is rare; editing the YAML is the normal path.

- `_config.yml` — course identity (name, code, semester, instructor, office hours),
  which links appear in the nav (`nav_pages`) and which external links show up
  (`link_github`, `link_gradescope`, `link_discussion` — blank hides them).
- `_data/schedule.yml` — one entry per week, rendered as the homepage schedule table.
  `status: normal | holiday | async | online` controls row styling and a badge next to
  the topic. `slides_url`/`lab_url` are optional — when empty the topic/lab render as
  plain text instead of links.
- `_data/announcements.yml`, `_data/assignments.yml`, `_data/resources.yml` — same
  pattern: flat lists of entries looped over in `index.html` / the matching page.
- `_layouts/default.html` — the single shared layout (navbar, mobile menu, footer).
  Every page's `content` is injected here; there are no other layouts.
- `assets/css/main.css` — the entire design system. Rebranding a duplicated copy of
  this site means editing this file, not the per-page HTML.
- Pages under `pages/` set their own front matter (`layout`, `title`, `permalink`) and
  otherwise pull identity strings from `site.*` — new pages should follow that pattern
  rather than hardcoding course info.
