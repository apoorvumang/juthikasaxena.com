# juthikasaxena.com

Personal site for Juthika Saxena. Built with [Astro](https://astro.build),
hosted on GitHub Pages at https://juthikasaxena.com.

---

## Setup on a new laptop

```bash
git clone https://github.com/apoorvumang/juthikasaxena.com.git
cd juthikasaxena.com
npm install
```

That's the one-time setup. From then on, just `cd` in and run commands.

---

## Run the site locally (preview before publishing)

```bash
npm run dev
```

Open http://localhost:4321. The site auto-reloads as you edit files.

To stop it, press `Ctrl+C` in the terminal.

---

## Publish a new post

There are two paths — pick whichever feels easier.

### A. Ask Claude Code (recommended)

Open Claude Code in this folder and say something like:

> "Publish a new post titled '*What motherhood taught me about prioritization*'.
> Here's the draft from my Google Doc: [paste the text]."

Claude Code will:
1. Convert the Google Doc text into clean markdown.
2. Create a new file under `src/content/writings/` with the right frontmatter.
3. Commit and push for you.
4. Confirm the deploy succeeded.

The site updates ~1–2 minutes after the push.

### B. Do it yourself

1. Create a new file `src/content/writings/<slug>.md` (use a URL-friendly slug,
   e.g. `motherhood-and-prioritization.md`).

2. Paste this template in and fill it out:

   ```md
   ---
   title: "What motherhood taught me about prioritization"
   description: "A short reflection on time, ambition, and choosing deliberately."
   category: "Motherhood"
   pubDate: 2026-05-12
   draft: false
   ---

   Body of the post in markdown.

   ## A heading

   Some prose, **bold**, *italic*, [a link](https://example.com).

   > A blockquote.

   - List item one
   - List item two
   ```

3. Optionally preview with `npm run dev` and check
   `http://localhost:4321/writings/<slug>`.

4. Commit and push:

   ```bash
   git add src/content/writings/<slug>.md
   git commit -m "Add post: What motherhood taught me about prioritization"
   git push
   ```

The site rebuilds automatically — usually live in 1–2 minutes.

---

## Frontmatter fields

Every post in `src/content/writings/` must start with a YAML block:

| Field         | Required | What it is                                                                                  |
| ------------- | -------- | ------------------------------------------------------------------------------------------- |
| `title`       | yes      | Post title shown on the listing and the post page.                                          |
| `description` | no       | One-line summary used on the listing page and in social previews.                           |
| `category`    | no       | Label shown above the title (e.g. `"Motherhood"`).                                          |
| `pubDate`     | yes      | Publish date in `YYYY-MM-DD` format. Posts sort newest-first.                               |
| `updatedDate` | no       | Last-edited date if you want to show it.                                                    |
| `draft`       | no       | `true` keeps the post hidden from the live site. Defaults to `false`.                       |

Suggested categories:
`Finance Transformation`, `AI Experiments`, `Consulting Notes`,
`Entrepreneurship`, `Motherhood`, `Fitness & Discipline`, `Personal Reflections`.

---

## Adding images to a post

1. Drop the image file into `public/writings-images/`.
2. Reference it in the markdown body with an absolute path:

   ```md
   ![Caption goes here](/writings-images/my-photo.jpg)
   ```

The headshot for the homepage is `public/headshot.jpeg` — replace that file
to update the photo.

---

## Updating the bio or homepage

All bio content (the "About" page) is in `src/pages/index.astro`. Edit the
text inside the `<p>`, `<h1>`, `<h2>`, etc. tags, save, and push. The cards
("Finance transformation", "AI experiments", etc.) are also in that file.

---

## Project structure

```
src/
  pages/
    index.astro              ← Homepage / bio
    writings/
      index.astro            ← Writings list page
      [...slug].astro        ← Individual post template
  content/
    config.ts                ← Frontmatter schema
    writings/                ← All blog posts (one .md file per post)
  layouts/Base.astro         ← Shared page shell (head, header, footer)
  components/                ← Header, BaseHead
  styles/global.css          ← Site-wide styles
public/
  headshot.jpeg              ← Bio photo
  CNAME                      ← Custom domain config (don't touch)
  writings-images/           ← Images used inside posts
.github/workflows/deploy.yml ← Auto-deploy config (don't touch)
```

---

## How deployment works

Every push to the `main` branch triggers
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml), which:

1. Builds the Astro site (`npm run build`)
2. Uploads the `dist/` folder to GitHub Pages
3. Site updates at https://juthikasaxena.com

Watch a deploy live at https://github.com/apoorvumang/juthikasaxena.com/actions.

---

## Troubleshooting

**Site didn't update after pushing**
- Check https://github.com/apoorvumang/juthikasaxena.com/actions — if the latest
  run is red, click in to see the error.
- Sometimes a cached version of the page sticks around in your browser.
  Hard-refresh (`Cmd+Shift+R` on Mac) or open in an incognito window.

**`npm run dev` fails**
- Make sure you ran `npm install` first.
- If still broken: `rm -rf node_modules package-lock.json && npm install`.

**Forgot the slug format**
- Lowercase, hyphens for spaces, no special characters.
  Good: `what-motherhood-taught-me.md`.
  Bad: `What Motherhood Taught Me!.md`.

---

## DNS / domain notes (rarely needed)

- Domain is registered at GoDaddy.
- DNS is managed at Cloudflare (nameservers `ashley/walt.ns.cloudflare.com`).
- DNS records must stay **"DNS only" (gray cloud)** in Cloudflare, *not*
  proxied (orange cloud). Proxy mode breaks GitHub Pages SSL cert
  provisioning.
