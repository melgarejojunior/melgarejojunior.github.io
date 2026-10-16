# Blog Melgarejo

Blog em português com Jekyll e o tema Minima, compatível com GitHub Pages. Sem painel administrativo: os artigos são arquivos Markdown. O conteúdo do repositório e do site será público.

## 1. Criar o repositório

1. Entre em https://github.com/new com a conta `melgarejojunior`.
2. Use o nome exato `melgarejojunior.github.io` e a visibilidade **Public**.
3. Crie o repositório. Extraia o ZIP do blog e envie o conteúdo da pasta `blog-melgarejo` para a raiz do repositório, usando **uploading an existing file**. Não envie a pasta externa nem o próprio ZIP.
4. Inclua a pasta `_posts` com seu artigo. Confirme que `_config.yml` e `index.md` estão na raiz e salve com **Commit changes**.
5. Em **Settings → Pages → Build and deployment**, selecione **Deploy from a branch**, branch `main`, pasta **/(root)** e **Save**.
6. Aguarde o processo de publicação. Confira o resultado em **Actions** e abra https://melgarejojunior.github.io.

Antes de publicar, personalize a descrição em `_config.yml`, a página `sobre.md` e edite ou exclua o artigo de exemplo.

## 2. Publicar artigos

No repositório, clique em **Add file → Create new file**. Use um nome como `_posts/2026-10-16-titulo-do-artigo.md`.

Cole este modelo e escreva abaixo do segundo `---`:

```markdown
---
layout: post
title: "Título do artigo"
date: 2026-10-16 09:00:00 -0400
---

O primeiro parágrafo aparece como resumo na página inicial.

## Uma seção

Continue o texto aqui.
```

Use a data real da publicação no nome e no campo `date`: artigos com data futura não aparecem até uma nova compilação depois dessa data. Clique em **Commit changes**; o Pages recompila o blog automaticamente. Para imagens, envie os arquivos para `assets/images/` e use `![Descrição da imagem]({{ '/assets/images/foto.jpg' | relative_url }})` no artigo.

## 3. Conectar melgarejo.net.br pela Cloudflare

Faça esta etapa depois de o endereço do GitHub funcionar. Se já existir outro site no domínio, a troca dos registros web muda o destino dele.

1. No GitHub, abra as configurações do perfil → **Pages**, adicione `melgarejo.net.br` e siga a verificação por registro TXT. Crie o TXT solicitado no DNS da Cloudflare e mantenha-o após a verificação.
2. No repositório, abra **Settings → Pages → Custom domain**, informe `melgarejo.net.br` e salve. O GitHub cria um arquivo `CNAME` na publicação por branch; preserve esse arquivo.
3. Na Cloudflare, em **DNS → Records**, configure os registros abaixo. Revise eventuais registros A, AAAA ou CNAME existentes para `@` e `www` que apontem para outro site. Preserve MX, registros de e-mail e o TXT de verificação.

| Tipo | Nome | Destino | Proxy |
| --- | --- | --- | --- |
| A | @ | 185.199.108.153 | DNS only |
| A | @ | 185.199.109.153 | DNS only |
| A | @ | 185.199.110.153 | DNS only |
| A | @ | 185.199.111.153 | DNS only |
| CNAME | www | melgarejojunior.github.io | DNS only |

Use a nuvem cinza (**DNS only**) nessa configuração. Nenhuma alteração no Registro.br é necessária se os nameservers já apontam para a Cloudflare.

4. Altere `url` no `_config.yml` para `"https://melgarejo.net.br"` e mantenha `baseurl: ""`.
5. Aguarde a validação do DNS e a emissão do certificado no GitHub. Marque **Enforce HTTPS** quando estiver disponível.
6. Teste `https://melgarejo.net.br`, `https://www.melgarejo.net.br`, a página Sobre, um artigo e o RSS. Com ambos os nomes configurados, o GitHub encaminha o www para o domínio principal.

Não ative um redirecionamento por regra da Cloudflare: o domínio será servido diretamente pelo Pages.

## Verificação local opcional

Com Ruby e Bundler instalados, execute `bundle install` e `bundle exec jekyll serve`. Abra o endereço local indicado no terminal. Esses programas não são necessários para publicar pelo GitHub.

## Referências

- https://docs.github.com/en/pages/quickstart
- https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages
