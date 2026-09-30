# Portfólio — Alef Ribeiro

Site estático de página única. HTML, CSS e JavaScript puros, sem build, sem dependência.
Basta subir a pasta em qualquer hospedagem.

```
index.html            página inteira
css/style.css         estilos
js/main.js            menu, scroll spy, reveal, vídeos sob demanda
assets/fonts/         Fraunces e Space Grotesk (locais, não dependem do Google)
assets/video/         vídeos dos estudos de caso
assets/img/           posters dos vídeos + og.jpg (imagem de compartilhamento)
assets/favicon.svg    ícone da aba
```

---

## Rodar local

```bash
powershell -NoProfile -ExecutionPolicy Bypass -File .claude/serve.ps1
```

Abre em <http://localhost:8850>. Qualquer servidor estático serve — abrir o `index.html`
direto pelo Explorer também funciona, só o carregamento das fontes fica menos previsível.

---

## O que falta preencher

Estes espaços estão marcados no site com a tarja **"Espaço reservado"**. O site já vai ao ar
sem eles; substitua conforme os arquivos ficarem prontos.

### 1. Foto do hero

Salve o retrato como `assets/img/alef.jpg` (vertical 4:5, luz quente) e, no `index.html`,
troque o bloco inteiro `<div class="slot slot--portrait">…</div>` por:

```html
<img src="assets/img/alef.jpg" alt="Alef Ribeiro" width="800" height="1000">
```

### 2. Peças gráficas (3 espaços)

Um em Origo, dois em DJ Alef. Jogue as imagens em `assets/img/` e troque cada
`<div class="slot slot--media">…</div>` por:

```html
<figure class="media">
  <img src="assets/img/nome-do-arquivo.jpg" alt="Descrição da peça">
  <figcaption>Legenda curta</figcaption>
</figure>
```

### 3. Imagem de compartilhamento

`assets/img/og.jpg` já existe. Depois do deploy, edite as duas `<meta>` no topo do
`index.html` trocando `https://alefribeiro.vercel.app/` pela URL real — redes sociais
não leem caminho relativo.

---

## Deploy

### Opção A — Vercel (mais rápido, recomendado)

1. Crie o repositório e o primeiro commit:

```bash
git init -b main && git add -A && git commit -m "Portfólio Alef Ribeiro"
```

2. Crie o repositório no GitHub e mande o código:

```bash
gh repo create portfolio-alef --public --source=. --push
```

*(Sem o `gh` instalado: crie o repo pelo site do GitHub e rode
`git remote add origin URL && git push -u origin main`.)*

3. Entre em <https://vercel.com>, **Add New → Project**, importe `portfolio-alef`.
   Framework Preset: **Other**. Build Command: deixe vazio. Output Directory: deixe vazio.
   Clique em **Deploy**.

4. Sai no ar em `portfolio-alef.vercel.app`. Em **Settings → Domains** dá pra trocar o
   subdomínio (ex.: `alefribeiro.vercel.app`) ou apontar um domínio próprio.

Cada `git push` daí em diante republica sozinho.

### Opção B — Netlify sem git

Entre em <https://app.netlify.com/drop> e arraste a pasta `portfolio-alef` inteira para a
página. Fica no ar em segundos. Para atualizar, arraste de novo.

### Opção C — GitHub Pages

Depois dos passos 1 e 2 acima: no repositório, **Settings → Pages → Source: Deploy from a
branch → main / (root) → Save**. Sai em `SEU-USUARIO.github.io/portfolio-alef`.

---

## Notas técnicas

- Os vídeos só baixam quando entram na tela (`preload="none"` + IntersectionObserver).
  O que aparece antes disso é o poster em JPG, com cerca de 60 KB cada.
- Se o navegador bloquear o autoplay, o vídeo fica no poster e toca ao clique.
- `prefers-reduced-motion` desliga animações, e sem JavaScript o conteúdo continua visível.
- Contraste de texto verificado para AA (mínimo 4.5:1) em todas as combinações de cor.
