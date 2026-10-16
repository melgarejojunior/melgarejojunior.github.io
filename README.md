# Melgarejo — bilingual blog

Jekyll + Minima on GitHub Pages. English is the default at `/en/`; Portuguese is at `/pt/`. The root forwards to English. Each article list only shows posts in its own language. RSS at `/feed.xml` includes both languages.

## Publish an article

Create a Markdown file in `_posts` named `YYYY-MM-DD-slug.md` with this header:

```yaml
---
layout: post
title: "Your title"
lang: en
translation_key: unique-article-name
permalink: /en/articles/your-slug/
date: 2026-10-15 12:00:00 -0400
---
```

Write the article below the header. The first paragraph becomes the excerpt. Use the actual publication date; future posts require a new build after their publication time. Commit to `main` to publish automatically.

For a Portuguese translation, create another file with `lang: pt-BR`, a Portuguese title, and `permalink: /pt/artigos/seu-titulo/`. Use the **same translation_key** in the two versions. Each key must have at most one document per language. The language switch appears only when a matching translation exists; a single-language article does not need a second file. Translations are edited manually.

Edit the home pages in `en/index.md` and `pt/index.md`, and About pages in `en/about.md` and `pt/sobre.md`. Navigation and dates follow the page language. Existing `/sobre/` and `/artigos/primeiro-artigo/` links forward to their Portuguese pages.

## Custom domain

The blog uses `https://blog.melgarejo.net.br`, with domain verification and Enforce HTTPS enabled in GitHub Pages. Keep the root `CNAME` file and `url` in `_config.yml` set to this subdomain; `baseurl` stays empty.

In Cloudflare, keep a DNS-only CNAME record named `blog` pointing to `melgarejojunior.github.io`, plus the GitHub domain-verification TXT record. The blog does not require changes to root, www, or email records.

Reference: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

## Local preview

With Ruby and Bundler installed: `bundle install`, then `bundle exec jekyll serve`.
