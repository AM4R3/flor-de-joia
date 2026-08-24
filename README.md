# Flor de Joia — landing page

Landing page de marca para **Flor de Joia** (semijoias · [@_flordejoia_](https://www.instagram.com/_flordejoia_/)).
Substitui o bio.site. HTML único, sem framework, sem build. Só o Google Fonts é externo.

**Objetivo de conversão**
1. Primário — entrar no Grupo VIP do WhatsApp (é onde a marca vende)
2. Secundário — WhatsApp direto para comprar/perguntar

---

## Imagens

Todas as fotos são **reais, tiradas do próprio grid do @_flordejoia_** e recortadas nas
regiões limpas de produto (fora dos textos sobrepostos dos posts). Nenhuma imagem de IA.

| Arquivo | O que é | Post de origem |
|---|---|---|
| `img/hero.jpg` | modelo com colar e anéis, fundo creme | 03/05/2026 |
| `img/olho-grego.jpg` | pulseira olho grego prata 925 sobre pedra clara | 22/07/2026 |
| `img/linha-fe.jpg` | pingente Nossa Senhora Aparecida em zircônias azuis | 22/07/2026 |
| `img/colecao-brasil.jpg` | chokers verde-esmeralda | 02/06/2026 |
| `og.jpg` | pulseira olho grego, 1200×630 — preview do WhatsApp | 22/07/2026 |

**Limitação de resolução:** o Instagram só serve 640px no grid público, então os
recortes têm entre 294px e 602px de largura. Renderizam bem, mas ficam levemente
suaves em telas retina. Se a dona tiver os originais, basta sobrescrever os arquivos
em `img/` com os mesmos nomes — as dimensões no HTML precisam ser atualizadas junto.

---

## Paleta — conferida contra o Instagram real

Amostrei as 12 imagens do grid e medi as cores por faixa de matiz, luminância e saturação.

| Token | Valor no site | Medido no grid | Veredito |
|---|---|---|---|
| `--blush` | `#F7E8E4` | `#F8E9E4` (fundo dos posts rosa) | ✅ praticamente exato |
| `--marinho` | `#1F2A44` | `#1E2D4A` (título "OLHO GREGO") | ✅ praticamente exato |
| `--dourado` | `#B99356` | `#B18B36`–`#B39B74` (scripts "Coleção") | ✅ dentro do cluster real |
| `--rosa` | `#BD7C76` | `#BD7872` / `#BC8479` (logotipo) | ➕ **adicionado** — faltava |
| `--creme` | `#F6EFE4` | `#FEEECD` / `#F3ECE6` / `#E6DFD9` | ➕ **adicionado** — faltava |

**Achado principal:** 83% da massa cromática dos posts está na faixa creme/dourado
(matiz 15–45) e só 10,5% no rosa. A marca roda **dois templates** em paralelo — um
blush/rosa e um creme/champanhe — e a versão inicial do site representava só o rosa.
Por isso a barra de confiança e a seção "Quem faz" passaram de branco puro para
`--creme`: as fotos de produto são predominantemente creme, e branco puro ao lado
delas lia frio.

`--rosa` (#BD7C76) tem 2,8:1 sobre o blush — **não passa em contraste nem como texto
grande**. Fica só em elemento decorativo (o glifo de flor dos filetes), nunca em texto.
Mesma regra do dourado.

### Divergência que vale a decisão da dona

Os posts usam **fonte manuscrita** ("protege", "acompanha", "Coleção", "nos detalhes").
O site não usa nenhuma, por decisão de projeto — script é o que mais faz marca pequena
parecer amadora no navegador, onde não há o controle de composição que existe num post.
Se ela quiser o script, dá pra reintroduzir só nos nomes de coleção, em tamanho grande.

Há também **dois logotipos diferentes** no grid: "Flor de Joia / SEMIJOIAS" com losango
(posts rosa) e "FLOR DE JÓIA" com flor de lótus (posts creme) — inclusive com grafia
diferente, *Joia* vs *Jóia*. O site usa "Flor de Joia" com o selo de 4 pétalas.
**Vale confirmar qual é o oficial.**

---

## Pendências antes de divulgar

| # | O que falta | Onde no `index.html` |
|---|---|---|
| 1 | **Número do WhatsApp** — trocar `wa.me/55SUBSTITUIR` pelo número real | 2 ocorrências: CTA final e barra sticky mobile |
| 2 | **Nome e história da fundadora** — do destaque "Sobre" do Instagram | seção `#sobre` |
| 3 | **Foto da fundadora** — não existe no grid público | seção `#sobre` |
| 4 | **Confirmar se o grupo é somente-admin** antes de manter "grupo silencioso, só a gente posta" | seção `#vip`, comentário `VALIDAR` |
| 5 | **Confirmar o logotipo oficial** (Joia vs Jóia, losango vs lótus) | nav e footer |

---

## Sistema de design

Tipografia: **Cormorant Garamond** (títulos, nomes de coleção em itálico) + **Jost** (corpo e UI).

Movimento: `cubic-bezier(0.22, 1, 0.36, 1)` a 0.5s. IntersectionObserver com fallback de 3s
(nada fica invisível se o observer falhar). `prefers-reduced-motion` reduz tudo a opacidade.

## Verificado

- Contraste WCAG AA: **0 reprovações** em todo o texto da página
- Alvos de toque de 44px em todos os links (área expandida via `::after`, sem mexer no visual)
- Sem overflow horizontal em 390px, 768px e 1280px
- Link do grupo idêntico e sem parâmetros de tracking nas 6 ocorrências

## Deploy

Estático puro — a Vercel serve a raiz sem build.
