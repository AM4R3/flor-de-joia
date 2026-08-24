# Flor de Joia — landing page

Landing page de marca para **Flor de Joia** (semijoias · [@_flordejoia_](https://www.instagram.com/_flordejoia_/)).
Substitui o bio.site. HTML único, sem framework, sem build. Só o Google Fonts é externo.

**Objetivo de conversão**
1. Primário — entrar no Grupo VIP do WhatsApp (é onde a marca vende)
2. Secundário — WhatsApp direto para comprar/perguntar

---

## Pendências antes de divulgar

| # | O que falta | Onde no `index.html` |
|---|---|---|
| 1 | **Número do WhatsApp** — trocar `wa.me/55SUBSTITUIR` pelo número real | 2 ocorrências: CTA final e barra sticky mobile |
| 2 | **Nome e história da fundadora** — do destaque "Sobre" do Instagram | seção `#sobre` |
| 3 | **Fotos reais de produto** — 1 hero + 3 de coleção + 1 da fundadora | comentários `SUBSTITUIR` |
| 4 | **`og.jpg`** (1200×630) na raiz — é o preview quando o link circular no WhatsApp | `<meta property="og:image">` |
| 5 | **Confirmar se o grupo é somente-admin** antes de manter "grupo silencioso, só a gente posta" | seção `#vip`, comentário `VALIDAR` |

Os placeholders de imagem são gradientes na paleta da marca — a página fica apresentável sem foto,
mas **foto real de produto converte mais que imagem de IA** numa página cujo produto é confiança.

### Como trocar uma foto

Cada bloco de imagem tem a tag `<img>` já escrita, comentada, com `alt` e dimensões:

```html
<div class="hero__media rv">
  <!-- SUBSTITUIR: ...
  <img src="img/hero-olho-grego.jpg" alt="..." width="1400" height="1750"> -->
</div>
```

Coloque o arquivo em `img/`, descomente a tag e apague o comentário. O gradiente fica atrás — some sozinho.

---

## Sistema de design

| Token | Valor | Uso |
|---|---|---|
| `--blush` | `#F7E8E4` | fundo dominante |
| `--rosa-po` | `#E8C4BC` | seção do Grupo VIP |
| `--marinho` | `#1F2A44` | texto e botão primário |
| `--dourado` | `#B99356` | **só filetes e ícones** — nunca texto |
| `--branco` | `#FFFFFF` | cards e barra de confiança |

Tipografia: **Cormorant Garamond** (títulos, nomes de coleção em itálico) + **Jost** (corpo e UI).
Nenhuma fonte manuscrita — é o que faz marca pequena parecer amadora.

Movimento: `cubic-bezier(0.22, 1, 0.36, 1)` a 0.5s. IntersectionObserver com fallback de 3s
(nada fica invisível se o observer falhar). `prefers-reduced-motion` reduz tudo a opacidade.

---

## Verificado

- Contraste WCAG AA: **0 reprovações** em todo o texto da página
- Alvos de toque de 44px em todos os links (área expandida via `::after`, sem mexer no visual)
- Sem overflow horizontal em 390px, 768px e 1280px
- Link do grupo idêntico e sem parâmetros de tracking nas 6 ocorrências
- Peso do HTML: ~33KB

## Deploy

Estático puro — a Vercel serve a raiz sem build.
