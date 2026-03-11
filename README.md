# Kenkyuu — Jekyll Site

Migrated from WordPress to Jekyll for GitHub Pages hosting at [gdfm.me](https://gdfm.me).

## Quick Start

```bash
# Install dependencies
bundle install

# Run locally
bundle exec jekyll serve

# Open http://localhost:4000
```

## Structure

```
.
├── _config.yml          # Site configuration
├── _layouts/            # HTML templates
│   ├── default.html
│   ├── home.html
│   ├── post.html
│   └── page.html
├── _posts/              # Blog posts (155 posts)
├── _pages/              # Static pages (about, research)
├── assets/
│   ├── css/main.css     # Stylesheet
│   ├── media/           # ← Unzip your WordPress media export here
│   └── pdfs/            # PDF files
├── _data/
│   └── attachments.txt  # List of original WordPress media URLs
├── CNAME                # Custom domain: gdfm.me
├── index.html           # Homepage (paginated post list)
└── 404.html
```

## Adding Your Media

1. Unzip your WordPress media export
2. Copy the contents into `assets/media/`
   - The folder structure should mirror WordPress uploads: `assets/media/2024/01/image.jpg`
3. All post images already reference `/assets/media/...` paths

For a full list of original attachment URLs, see `_data/attachments.txt`.

## Deploy to GitHub Pages

1. Create a repo named `<yourusername>.github.io` (or use an existing repo)
2. Push this folder to the `main` branch
3. In repo Settings → Pages → Source: `main` branch, `/ (root)`
4. Add your custom domain in Settings → Pages → Custom domain: `gdfm.me`
5. Update DNS:
   - A records pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - CNAME `www` → `<yourusername>.github.io`

## Plugins Used

- `jekyll-feed` — RSS feed at `/feed.xml`
- `jekyll-seo-tag` — Meta tags for SEO
- `jekyll-sitemap` — Sitemap at `/sitemap.xml`
- `jekyll-paginate` — 10 posts per page on homepage

All plugins are on GitHub Pages' [safe list](https://pages.github.com/versions/).
