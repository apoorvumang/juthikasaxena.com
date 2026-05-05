# juthikasaxena.com

Personal site for Juthika Saxena. Built with [Astro](https://astro.build).

## Run locally

```bash
npm install
npm run dev
```

Then open http://localhost:4321.

## Project structure

```
src/
  pages/
    index.astro            # About page
    writings/
      index.astro          # Writings list
      [...slug].astro      # Individual post template
  content/
    config.ts              # Frontmatter schema
    writings/              # Markdown posts go here
  layouts/Base.astro       # Shared page shell
  components/              # Header, BaseHead
  styles/global.css        # Site-wide styles
public/                    # Static assets (headshot, CNAME, favicon)
```

## Adding a writing

Drop a markdown file in `src/content/writings/`:

```md
---
title: "Title goes here"
description: "One-line summary for the listing page."
category: "Finance Transformation"
pubDate: 2026-05-12
draft: false
---

Body of the post in markdown.
```

Set `draft: true` to keep it out of the live site.

## Deployment

Pushes to `main` build via GitHub Actions and deploy to GitHub Pages at
`https://juthikasaxena.com`.
