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

## Custom domain — not connected yet

1. Verify `melgarejo.net.br` in your GitHub profile → Settings → Pages, using the TXT record GitHub provides in Cloudflare.
2. Set `melgarejo.net.br` in this repository → Settings → Pages → Custom domain, before changing DNS. Keep the CNAME file GitHub creates.
3. In Cloudflare, use DNS-only A records for `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`. Point CNAME `www` to `melgarejojunior.github.io`, also DNS only. Preserve email records and review existing web records before replacing them.
4. Change `url` in `_config.yml` to `https://melgarejo.net.br`. Keep `baseurl` empty.
5. Wait for the DNS check and HTTPS certificate; enable Enforce HTTPS. Test both languages and www.

Reference: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

## Local preview

With Ruby and Bundler installed: `bundle install`, then `bundle exec jekyll serve`.
