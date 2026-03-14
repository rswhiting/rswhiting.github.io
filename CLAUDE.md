# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Serve locally with live reload
jekyll serve

# Build the site
jekyll build
```

The site builds to `_site/` (gitignored). GitHub Pages handles production deployment automatically on push to `master`.

## Architecture

This is a **Jekyll static blog** based on the Codinfox-Lanyon theme, hosted at `rswhiting.com`.

**Content flow:** Markdown posts in `_posts/` → Jekyll processes with Liquid templates from `_layouts/` and `_includes/` → static HTML output in `_site/`.

**Styling flow:** `_scss/` source files → compiled through `public/css/main.scss` → CSS output.

### Key files

- `_config.yml` — Site metadata, plugins, permalink structure, pagination (5 posts/page)
- `_config.scss` — Theme color and layout variables
- `_layouts/default.html` — Master layout with sidebar; `post.html` and `page.html` extend it
- `_includes/sidebar.html` — Navigation sidebar with links defined in `_config.yml`
- `public/css/main.scss` — Main stylesheet entry point (imports from `_scss/`)

### Adding content

**New blog post:** Create `_posts/YYYY-MM-DD-slug.md` with front matter:
```yaml
---
layout: post
title: "Post Title"
description: "Short description"
category: categoryname
tags: [tag1, tag2]
---
```

Use `<!-- more -->` to set the excerpt break point.

**Images:** Most images are linked directly from the Google Photos album "Blog Public" (public view access) rather than stored in the repo. A small number of older images live in `public/images/YYYY/` and are referenced as `/public/images/YYYY/filename.jpg`.

**Special pages** (not posts): Create as `.md` files in the root with `layout: page`.

## Writing Collaboration

Use the `writer` agent (available globally) when helping draft or edit blog posts, essays, or other publications. It captures Robert's voice and collaboration preferences.
