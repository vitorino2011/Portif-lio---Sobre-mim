# Portfólio — Documentação HTML Completa

**Arquivo:** `index.html`  
**Título:** João Vitor Ramos — Portfólio  
**Idioma:** `pt-BR`  
**Autor:** João Vitor Ramos Vitorino

---

## Sumário

1. [Visão Geral](#1-visão-geral)
2. [Estrutura de Arquivos Externos](#2-estrutura-de-arquivos-externos)
3. [Head — Meta e Fontes](#3-head--meta-e-fontes)
4. [SVG Gradientes Globais](#4-svg-gradientes-globais)
5. [Elementos Fixos da Página](#5-elementos-fixos-da-página)
6. [Seção: Navbar](#6-seção-navbar)
7. [Seção: Hero](#7-seção-hero)
8. [Seção: About](#8-seção-about)
9. [Modal: Minha História (Story)](#9-modal-minha-história-story)
10. [Modal: Vídeo](#10-modal-vídeo)
11. [Seção: Quote](#11-seção-quote)
12. [Seção: Journey (Timeline)](#12-seção-journey-timeline)
13. [Seção: Tablet Scroll (Code Section)](#13-seção-tablet-scroll-code-section)
14. [Seção: Skills](#14-seção-skills)
15. [Seção: Contact](#15-seção-contact)
16. [Footer](#16-footer)
17. [Scripts Inline](#17-scripts-inline)
18. [Fluxo de Interações](#18-fluxo-de-interações)
19. [IDs Importantes](#19-ids-importantes)
20. [Assets Necessários](#20-assets-necessários)

---

## 1. Visão Geral

Página única (`SPA`-like) de portfólio pessoal. Todo o CSS está embutido em `<style>` dentro do `<head>`, e todos os scripts estão em um único bloco `<script>` no final do `<body>`. Não há dependências externas além das fontes do Google Fonts e ícones do `devicons` via jsDelivr CDN.

**Mapa de seções em ordem de aparição:**

| Ordem | ID / Elemento | Descrição |
|-------|--------------|-----------|
| 1 | Globais | `#cursorGlow`, `#particles`, `#progressBar` |
| 2 | `#navbar` | Barra de navegação fixa |
| 3 | `#home` | Hero — cartão 3D + texto de apresentação |
| 4 | `#about` | Sobre — cards de info + botão de história |
| 5 | `#storyOverlay` | Modal overlay — história pessoal |
| 6 | `#videoOverlay` | Modal overlay — player de vídeo |
| 7 | `.quote-section` | Citação pessoal |
| 8 | `#journey` | Timeline da jornada de aprendizado |
| 9 | `#codeSection` | Tablet scroll com editor de código |
| 10 | `#skills` | Grade de habilidades com barras |
| 11 | `#contact` | Botões de contato |
| 12 | `footer` | Rodapé com links e copyright |

---

## 2. Estrutura de Arquivos Externos

O projeto depende dos seguintes recursos externos e locais:

**Fontes (Google Fonts CDN):**
```html
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600&display=swap');
```

| Fonte | Uso |
|-------|-----|
| `Inter` | Fonte principal de toda a página |
| `JetBrains Mono` | Código, badges de linguagem, timer do vídeo |

**Ícones de tecnologia (jsDelivr CDN):**

| URL | Ícone |
|-----|-------|
| `devicons/arduino/arduino-original.svg` | Arduino |
| `devicons/cplusplus/cplusplus-original.svg` | C++ |
| `devicons/python/python-original.svg` | Python |
| `devicons/html5/html5-original.svg` | HTML5 |
| `devicons/css3/css3-original.svg` | CSS3 |
| `devicons/javascript/javascript-original.svg` | JavaScript |

**Imagens locais** (precisam estar na mesma pasta do `index.html`):

| Arquivo | Onde é usado |
|---------|-------------|
| `WhatsApp Image 2026-03-01 at 23.08.20.jpeg` | Foto principal no cartão 3D e no story modal |
| `WhatsApp Image 2026-03-01 at 10.54.53 copy.jpeg` | Avatar pequeno dentro do card overlay |

> ⚠️ Os nomes de arquivo contêm espaços. Em produção, renomear para `foto-principal.jpg` e `avatar.jpg` e atualizar os `src` correspondentes.

---

## 3. Head — Meta e Fontes

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>João Vitor Ramos — Portfólio</title>
```

- `charset="UTF-8"` garante suporte a caracteres especiais em português
- `viewport` com `initial-scale=1.0` habilita responsividade em dispositivos móveis
- `<title>` é o texto exibido na aba do navegador e em resultados de busca

---

## 4. SVG Gradientes Globais

Bloco `<svg>` invisível no topo do `<body>`, define gradientes reutilizáveis em toda a página via `fill="url(#id)"`:

```html
<svg style="position:absolute;width:0;height:0">
  <defs>
    <linearGradient id="igGrad" ...>   <!-- Gradiente roxo-vermelho do Instagram -->
    <linearGradient id="gitGrad" ...>  <!-- Gradiente laranja-vermelho do Git -->
  </defs>
</svg>
```

**`igGrad`** — 5 paradas de cor que reproduzem o gradiente oficial do Instagram:

| Posição | Cor |
|---------|-----|
| 0% | `#f09433` (laranja) |
| 25% | `#e6683c` |
| 50% | `#dc2743` (vermelho) |
| 75% | `#cc2366` |
| 100% | `#bc1888` (roxo) |

**`gitGrad`** — Gradiente do Git/GitLens:

| Posição | Cor |
|---------|-----|
| 0% | `#f34f29` (laranja Git) |
| 100% | `#d13d2f` |

Esses gradientes são referenciados nos ícones SVG de Instagram e Git dentro dos cartões, na navbar, no footer e na timeline.

---

## 5. Elementos Fixos da Página

Três elementos ficam sempre visíveis independente do scroll:

### Cursor Glow
```html
<div class="cursor-glow" id="cursorGlow"></div>
```
Círculo de 400×400px que segue o cursor. Começa com `opacity: 0` e é ativado via JS no `mousemove`.

### Particles
```html
<div class="particles" id="particles"></div>
```
Container vazio que o JS popula com 30 `<div class="particle">` ao carregar a página.

### Progress Bar
```html
<div class="progress-bar" id="progressBar"></div>
```
Barra de 2px fixada abaixo da navbar. Largura de `0%` a `100%` conforme o scroll.

---

## 6. Seção: Navbar

```html
<nav class="navbar" id="navbar">
```

**Estrutura interna:**

```
nav.navbar
  ├── div.nav-logo          ← "João Vitor Ramos Vitorino"
  ├── ul.nav-links#navLinks ← Links: Sobre, Jornada, Skills, Contato
  └── div (wrapper)
        ├── div.nav-social  ← Ícones GitHub e Instagram
        └── button.mobile-toggle#mobileToggle ← Hambúrguer (SVG de 3 linhas)
```

**Links de navegação:**

| Texto | `href` | Destino |
|-------|--------|---------|
| Sobre | `#about` | Seção About |
| Jornada | `#journey` | Seção Timeline |
| Skills | `#skills` | Seção Skills |
| Contato | `#contact` | Seção Contact |

> Os cliques nesses links são interceptados via JS com `scrollIntoView({ behavior: 'smooth' })`. O `href` serve como referência ao seletor, não como âncora HTML nativa.

**Comportamento responsivo:**
- Em desktop: `ul.nav-links` fica visível como linha horizontal
- Em mobile (≤900px): `ul.nav-links` fica `display: none`; o botão hambúrguer aparece
- Ao clicar no hambúrguer, o JS alterna a classe `open` em `#navLinks`, que força `display: flex` com posicionamento absoluto abaixo da navbar

---

## 7. Seção: Hero

```html
<section class="hero" id="home">
```

**Camadas de fundo (ordem de empilhamento):**

```
section.hero
  ├── div.hero-bg        ← Gradientes radiais decorativos (pointer-events: none)
  ├── div.hero-grid-bg   ← Grade de linhas 60×60px (pointer-events: none)
  └── div.hero-content   ← Conteúdo principal (z-index: 2)
```

### Cartão 3D (lado esquerdo do hero)

```
div.card-3d-wrapper#card3dWrapper   ← perspective: 1200px; recebe mousemove
  └── div.card-3d#card3d            ← recebe transform rotateX/Y via JS
        ├── img.card-3d-img         ← Foto principal (grayscale 20% → 0% no hover)
        ├── div.card-3d-shine#cardShine  ← Brilho radial (var --mx, --my)
        ├── div.card-3d-border      ← Borda sutil permanente (z-index: 11)
        └── div.card-overlay        ← Painel que expande da esquerda (width: 0 → 100%)
              └── div.card-overlay-inner  ← Conteúdo com delay de 0.18s
                    ├── div.card-profile-row
                    │     ├── div.card-avatar (img avatar pequeno)
                    │     └── div.card-profile-info (nome + cargo)
                    ├── div.card-langs    ← Badges: C++, Python, JS, HTML, CSS, Arduino, Git
                    ├── div.card-bio      ← Frase curta de apresentação
                    ├── div.card-location ← Ícone de pin + "MS, Brasil"
                    ├── div.card-stats    ← 3 stats: 14 Anos / 5+ Linguagens / MS
                    └── div.card-socials  ← Links GitHub e Instagram
```

### Texto Hero (lado direito)

```
div.hero-text
  ├── div.hero-greeting.reveal        ← "Olá, eu sou"
  ├── h1.hero-heading.reveal          ← "João Vitor\nRamos"
  ├── p.hero-desc.reveal              ← Apresentação com <strong> destacados
  └── div.hero-cta.reveal
        ├── a.btn.btn-primary → #skills   ← "Ver Projetos"
        └── a.btn.btn-outline → GitHub    ← "GitHub ↗"
```

**Scroll Hint:**
```html
<div class="scroll-hint">
  <span>SCROLL</span>
  <svg>↓</svg>  <!-- Seta animada com scrollBounce -->
</div>
```
Posicionado absolutamente no `bottom: 40px` da hero section.

---

## 8. Seção: About

```html
<section class="section" id="about">
```

**Estrutura:**

```
section#about
  ├── div.section-label.reveal       ← "Sobre mim"
  ├── h2.section-heading.reveal      ← "Quem Sou Eu"
  ├── p.section-desc.reveal          ← Texto de introdução
  ├── div.about-grid                 ← Grid 4 cards
  │     ├── .about-card (14 Anos)
  │     ├── .about-card (Robótica)
  │     ├── .about-card (5+ Linguagens)
  │     └── .about-card (MS, Brasil)
  └── div.story-trigger.reveal       ← Botão "Minha História"
        └── div.story-trigger-content
              ├── svg (ícone de livro)
              ├── div.story-trigger-text (h3 + p)
              └── div.story-trigger-arrow (seta →)
```

**Cards do about-grid:**

| Card | Ícone (SVG) | Título | Subtítulo |
|------|------------|--------|-----------|
| 1 | Pessoa/círculo | 14 Anos | Jovem e determinado |
| 2 | Camadas/stack | Robótica | Onde tudo começou |
| 3 | Code `</>` | 5+ Linguagens | E contando... |
| 4 | Pin de localização | MS, Brasil | Mato Grosso do Sul |

**Story trigger:**
- `onclick="openStory()"` chama a função JS que exibe o `#storyOverlay`
- Animação hover: `scale(1.02)` + brilho radial central + seta escala `1.1x`

---

## 9. Modal: Minha História (Story)

```html
<div class="story-overlay" id="storyOverlay" onclick="if(event.target===this)closeStory()">
```

> O `onclick` no overlay verifica `event.target===this` — fecha apenas se clicar no fundo escuro, não no modal em si.

**Estrutura interna:**

```
div.story-overlay#storyOverlay
  └── div.story-modal
        ├── div.story-modal-header (sticky top:0)
        │     ├── h2 "Minha História"
        │     └── div.story-modal-actions
        │           ├── button.modal-btn-video → onclick="openVideo()"
        │           └── button.modal-btn-close → onclick="closeStory()"
        └── div.story-modal-body
              ├── div.story-modal-text
              │     └── 5x <p> com a história em detalhes
              └── div.story-modal-img
                    └── img (foto principal)
```

**Conteúdo dos parágrafos:**

| Parágrafo | Tema |
|-----------|------|
| 1 | Apresentação — nome, idade, origem e início na robótica |
| 2 | Arduino — curso de 1 ano, eletrônica, programação embarcada |
| 3 | Python — transição, Gustavo Guanabara, Curso em Vídeo |
| 4 | C++ avançado — Bruno Pinho Campos, Git e GitHub |
| 5 | Visão de futuro — tecnologia como ferramenta de transformação |

**Como abrir/fechar:**

| Ação | Como |
|------|------|
| Abrir | `openStory()` — chamada pelo `.story-trigger` |
| Fechar | `closeStory()` — botão fechar OU clique no fundo |
| Ir para vídeo | Botão "Reproduzir Vídeo" → `openVideo()` |

---

## 10. Modal: Vídeo

```html
<div class="video-overlay" id="videoOverlay" onclick="if(event.target===this)closeVideo()">
```

**Estrutura completa:**

```
div.video-overlay#videoOverlay
  └── div.video-container
        ├── div.video-top-bar
        │     ├── span "Sobre João Vitor Ramos"
        │     └── div.video-close-btn → onclick="closeVideo()"
        ├── div.video-wrapper#videoWrapper
        │     ├── div.video-placeholder#videoPlaceholder
        │     │     ├── svg (ícone play)
        │     │     ├── p "Adicione seu vídeo MP4 aqui"
        │     │     └── label.btn (input type="file" oculto)
        │     │           └── input#videoInput type="file" accept="video/mp4"
        │     └── video#mainVideo (display:none inicialmente)
        └── div.video-controls
              ├── .vc-btn → skipVideo(-10)      ← Voltar 10s
              ├── .vc-btn#playBtn → togglePlay() ← Play/Pause
              ├── .vc-btn → skipVideo(10)        ← Avançar 10s
              ├── .vc-progress#vcProgress → seekVideo(event)
              │     └── .vc-progress-fill#vcFill
              ├── .vc-time#vcTime               ← "0:00 / 0:00"
              ├── .vc-speed#vcSpeed → changeSpeed() ← "1x"
              ├── .vc-btn → goFullscreen()       ← Tela cheia
              └── .vc-like#vcLike → toggleLike()
                    └── span.vc-like-count#likeCount
```

**Fluxo de carregamento do vídeo:**
1. Usuário clica no `<label>`, que ativa o `<input type="file">` oculto
2. `onchange="loadVideo(this)"` cria uma URL local com `URL.createObjectURL()`
3. A URL é injetada em `video#mainVideo` via `.src`
4. O placeholder é ocultado (`display: none`)
5. Listeners de `loadedmetadata` e `timeupdate` são adicionados ao vídeo
6. A barra `#vcFill` e o texto `#vcTime` passam a ser atualizados em tempo real

**z-index dos modais:**
- `#storyOverlay`: `z-index: 2000`
- `#videoOverlay`: `z-index: 3000` — fica acima do story para poder ser aberto a partir dele

---

## 11. Seção: Quote

```html
<div class="quote-section">
```

Seção minimalista centralizada entre a seção About e a Journey:

```
div.quote-section
  ├── div.quote-mark.reveal          ← Símbolo " (opacity: 0.1)
  ├── p.quote-text.reveal            ← Citação com <strong> destacados
  └── div.quote-author.reveal        ← "— João Vitor Ramos"
```

> Citação: *"A tecnologia não é apenas uma ferramenta — é uma forma de pensar e transformar o mundo ao nosso redor."*

---

## 12. Seção: Journey (Timeline)

```html
<section class="section" id="journey">
```

**Estrutura da timeline:**

```
section#journey
  ├── div.section-label.reveal       ← "Minha jornada"
  ├── h2.section-heading.reveal      ← "Linha do Tempo"
  ├── p.section-desc.reveal
  └── div.timeline
        ├── div.timeline-item.reveal (2024 — O Início)
        ├── div.timeline-item.reveal (2024 — Primeira Linguagem)
        ├── div.timeline-item.reveal (2024 — Evolução)
        ├── div.timeline-item.reveal (2025 — Web)
        └── div.timeline-item.reveal (Atualmente — Versionamento)
```

**Cada `timeline-item` contém:**
```
div.timeline-item
  ├── div.timeline-year    ← Período e subtítulo
  ├── h3.timeline-title    ← Ícone (img ou svg) + Título
  └── p.timeline-text      ← Descrição detalhada com <strong>
```

**Linha do Tempo detalhada:**

| Período | Título | Ícone | Destaque |
|---------|--------|-------|---------|
| 2024 — O Início | Robótica & Microcontroladores | Arduino SVG | Curso de 1 ano, eletrônica, embarcados |
| 2024 — Primeira Linguagem | Arduino & C++ Intermediário | C++ SVG | Sensores, atuadores, estruturas de controle |
| 2024 — Evolução | Python — Automação & Lógica | Python SVG | Curso em Vídeo, Gustavo Guanabara |
| 2025 — Web | HTML, CSS & JavaScript | HTML5 SVG | HTML semântico, CSS moderno, JS interativo |
| Atualmente | Git & Versionamento | Git SVG (gitGrad) | Commits, branches, merge, GitHub |

**Animação do ponto da timeline:**
- Em repouso: `background: #333`, `border: 2px solid #555`
- Quando `.visible` (via IntersectionObserver): `background: #fff`, `box-shadow: 0 0 20px rgba(255,255,255,.3)` — o ponto "acende"

---

## 13. Seção: Tablet Scroll (Code Section)

```html
<div class="tablet-scroll-section" id="codeSection">
```

A seção mais complexa estruturalmente. Combina scroll-driven animation com um editor de código simulado.

**Estrutura completa:**

```
div.tablet-scroll-section#codeSection
  ├── div.tablet-scroll-intro
  │     └── div.section-label.reveal "Projetos em código"
  └── div.tablet-scroll-container#tabletScrollContainer  ← height: 220vh
        └── div.tablet-sticky-wrapper  ← position: sticky; top: 0; height: 100vh
              └── div.tablet-content-inner
                    ├── div.tablet-anim-header#tabletAnimHeader
                    │     ├── div.tab-label (oculto — sem texto visível)
                    │     └── h2 "Meu Código, <span.highlight>Minha Identidade</span>"
                    └── div.tablet-card-container#tabletAnimCard
                          └── div.tablet-card
                                └── div.tablet-inner-screen
                                      ├── div.tablet-os-bar
                                      │     ├── div.tablet-os-dots (td1 td2 td3)
                                      │     ├── div.tablet-os-title "joao-vitor-ramos — editor"
                                      │     └── div.tablet-os-file#tabletFileName
                                      ├── div.tablet-tabs
                                      │     ├── button.tablet-tab.active → python
                                      │     ├── button.tablet-tab → cpp
                                      │     ├── button.tablet-tab → html
                                      │     ├── button.tablet-tab → css
                                      │     ├── button.tablet-tab → js
                                      │     └── button.tablet-tab → git
                                      └── div.tablet-panels
                                            ├── div.tablet-panel.active#tpanel-python
                                            ├── div.tablet-panel#tpanel-cpp
                                            ├── div.tablet-panel#tpanel-html
                                            ├── div.tablet-panel#tpanel-css
                                            ├── div.tablet-panel#tpanel-js
                                            └── div.tablet-panel#tpanel-git
```

**Conteúdo de cada painel de código:**

| ID do Painel | Linguagem | Conteúdo |
|-------------|-----------|---------|
| `tpanel-python` | Python | Classe `Developer` com `__init__`, `dream()` e `greet()` — dados pessoais como atributos |
| `tpanel-cpp` | C++ / Arduino | `struct Developer` com `setup()` e `loop()` — sketch Arduino com dados pessoais |
| `tpanel-html` | HTML | Estrutura básica de página com `<header>`, `<nav>`, `<main>`, `<section>` |
| `tpanel-css` | CSS | `:root` com variáveis + estilos de `.hero` e `.btn-primary` |
| `tpanel-js` | JavaScript | Objeto `dev` com `greet()`, `learnMore()` e listener de scroll |
| `tpanel-git` | Git | Simulação de `git log --oneline`, `git status` e `git push` |

**Syntax highlighting via classes HTML:**

Cada trecho de código no painel usa `<span>` com classes de cor:

| Classe | Cor | Representa |
|--------|-----|-----------|
| `.kw` | `#c9a0dc` | Palavras-chave (`def`, `class`, `self`, `const`) |
| `.str` | `#a8cc8c` | Strings entre aspas |
| `.fn` | `#6cb6ff` | Nomes de funções e métodos |
| `.cm` | `#555` | Comentários (`#`, `//`) |
| `.tag` | `#e06c75` | Tags HTML |
| `.attr` | `#d19a66` | Atributos e nomes de propriedades |
| `.val` | `#98c379` | Valores de atributos HTML / CSS |
| `.num` | `#d19a66` | Números literais |
| `.prop` | `#56b6c2` | Propriedades CSS e tipos C++ |

**Dots da OS bar:**

| Classe | Cor | Representa |
|--------|-----|-----------|
| `.td1` | `#ff5f57` | Fechar (vermelho macOS) |
| `.td2` | `#febc2e` | Minimizar (amarelo macOS) |
| `.td3` | `#28c840` | Maximizar (verde macOS) |

---

## 14. Seção: Skills

```html
<section class="section" id="skills">
```

**Estrutura:**

```
section#skills
  ├── div.section-label.reveal       ← "Habilidades"
  ├── h2.section-heading.reveal      ← "Linguagens & Tecnologias"
  ├── p.section-desc.reveal
  └── div.skills-grid                ← Grid 3 colunas (auto-fit minmax 300px)
        ├── div.skill-card.reveal (C++ / Arduino)
        ├── div.skill-card.reveal (Python)
        ├── div.skill-card.reveal (HTML5)
        ├── div.skill-card.reveal (CSS3)
        ├── div.skill-card.reveal (JavaScript)
        └── div.skill-card.reveal (Git)
```

**Cada `skill-card` contém:**

```
div.skill-card
  ├── div.skill-icon    ← img ou svg da tecnologia (56×56px)
  ├── h3                ← Nome da tecnologia
  ├── p                 ← Descrição curta
  ├── div.skill-tags    ← Badges de tags relacionadas
  ├── div.skill-level   ← "<nível>  <percentual%>"
  └── div.skill-bar-track
        └── div.skill-bar-fill[data-width="XX"]  ← Animada via JS
```

**Dados completos das skills:**

| Skill | Nível | % | Tags |
|-------|-------|---|------|
| C++ / Arduino | Intermediário | 60% | Arduino IDE, OOP, Sensores, Atuadores |
| Python | Intermediário | 55% | Automação, Scripts, Lógica |
| HTML5 | Intermediário | 65% | Semântico, Formulários, A11y |
| CSS3 | Intermediário | 60% | Flexbox, Grid, Animações |
| JavaScript | Básico | 35% | DOM, Eventos, ES6+ |
| Git | Básico | 40% | Commits, Branches, GitHub |

**Como a barra anima:**
- Em repouso (antes de entrar na viewport): `width: 0`
- Ao `.visible` (IntersectionObserver): JS lê `data-width` e aplica como `style.width = "XX%"`
- A transição CSS é `1.5s cubic-bezier(.16,1,.3,1)` — efeito de mola suave
- Ao sair da viewport, a classe `.visible` é removida e a barra volta a `0` (pronta para reanimar)

**Glow interativo:**
- `mousemove` no card atualiza `--mx` e `--my` com a posição do cursor em porcentagem
- O CSS usa essas variáveis em `radial-gradient` via `::before` com `opacity: 0 → 1` no hover

---

## 15. Seção: Contact

```html
<section class="section" id="contact" style="text-align:center">
```

Seção simples e centralizada com dois botões de ação direta:

```
section#contact
  ├── div.section-label.reveal        ← "Vamos conversar"
  ├── h2.section-heading.reveal       ← "Entre em Contato"
  ├── p.section-desc.reveal           ← Texto de convite
  └── div.reveal (flex, justify-center)
        ├── a.btn.btn-primary → GitHub  ← Ícone GitHub + "GitHub"
        └── a.btn.btn-outline → Instagram ← Ícone Instagram + "Instagram"
```

Ambos os links abrem em `target="_blank"` (nova aba).

---

## 16. Footer

```html
<footer class="footer">
```

```
footer.footer
  └── div.footer-content
        ├── div.footer-socials
        │     ├── a → GitHub (SVG)
        │     └── a → Instagram (SVG)
        ├── p.footer-text
        │     └── "© 2026 João Vitor Ramos. Todos os direitos reservados."
        └── div.footer-links
              ├── a → GitHub
              ├── a → Instagram
              └── a href="#home" → "Voltar ao topo ↑"
```

O link "Voltar ao topo" usa âncora HTML nativa (`href="#home"`), diferente dos nav links que usam JS.

---

## 17. Scripts Inline

Todo o JavaScript está em um único bloco `<script>` no final do `<body>`. Dividido em módulos comentados com `// ═══ NOME ═══`:

| Módulo | O que faz |
|--------|-----------|
| `PARTICLES` | Gera 30 partículas flutuantes dinamicamente |
| `3D HERO CARD` | Rotação 3D do cartão via `mousemove` |
| `SKILL CARD GLOW` | Glow radial que segue o cursor nos skill cards |
| `SCROLL REVEAL` | `IntersectionObserver` para animações de entrada/saída |
| `PROGRESS BAR + NAVBAR` | Atualiza barra de progresso e classe `scrolled` da navbar |
| `CURSOR GLOW` | Halo suave que segue o cursor pelo documento |
| `NAV LINKS` | Scroll suave + toggle do menu mobile |
| `STORY & VIDEO MODALS` | Abertura, fechamento e player de vídeo completo |
| `LIKE SYSTEM` | Curtir/descurtir com persistência em `localStorage` |
| `TABLET CODE SWITCHER` | Alterna painéis e nome do arquivo no editor |
| `TABLET SCROLL ANIMATION` | Animação 3D scroll-driven com `requestAnimationFrame` |

> Para documentação detalhada de cada módulo JS, consulte `portfolio-scripts.md`.

---

## 18. Fluxo de Interações

```
Usuário abre a página
  └── JS executa após carregamento
        ├── Gera 30 partículas
        ├── Inicia IntersectionObserver (reveal + skill bars)
        ├── Inicia scroll listeners (progress bar + navbar + tablet animation)
        ├── Aplica .visible nos .reveal da hero após 200ms
        └── Carrega likes do localStorage

Usuário rola a página
  ├── .reveal e .timeline-item animam ao entrar na viewport
  ├── .skill-bar-fill animam com largura do data-width
  ├── Tablet card rotaciona de 22° → 0° e escala
  ├── Tablet header sobe -110px e fade out
  └── Barra de progresso atualiza

Usuário hover no cartão 3D
  ├── Overlay expande de 0% → 100% (width animation)
  ├── Conteúdo interno desliza de translateX(-24px) → 0
  ├── Shine radial aparece seguindo o cursor
  └── Foto escala 1.05x e remove grayscale

Usuário clica em "Minha História"
  └── openStory()
        ├── display: flex no #storyOverlay
        ├── requestAnimationFrame → adiciona .active (opacity + scale)
        └── body overflow: hidden

  Dentro do story modal
  └── Usuário clica "Reproduzir Vídeo"
        └── openVideo() (z-index: 3000, sobre o story)
              └── Usuário carrega arquivo MP4
                    └── loadVideo() cria URL local e ativa controles

Usuário interage com video player
  ├── togglePlay() — alterna play/pause e ícone do botão
  ├── skipVideo(±10) — pula 10 segundos
  ├── seekVideo(e) — clica na barra para ir a um ponto
  ├── changeSpeed() — cicla entre 0.5x, 0.75x, 1x, 1.25x, 1.5x, 2x
  ├── goFullscreen() — entra em tela cheia
  └── toggleLike() — curtir/descurtir com persistência localStorage
```

---

## 19. IDs Importantes

Referência rápida de todos os `id` usados por JavaScript:

| ID | Tipo | Usado por |
|----|------|-----------|
| `cursorGlow` | `div` | Cursor glow JS |
| `particles` | `div` | Particles generator JS |
| `progressBar` | `div` | Scroll progress JS |
| `navbar` | `nav` | Navbar scrolled class JS |
| `card3dWrapper` | `div` | 3D card mousemove listener |
| `card3d` | `div` | 3D card transform receiver |
| `cardShine` | `div` | Shine CSS var updater |
| `navLinks` | `ul` | Mobile menu toggle |
| `mobileToggle` | `button` | Mobile menu button |
| `storyOverlay` | `div` | Story modal open/close |
| `videoOverlay` | `div` | Video modal open/close |
| `videoWrapper` | `div` | Fullscreen target |
| `videoPlaceholder` | `div` | Hidden after video load |
| `videoInput` | `input` | File picker for video |
| `mainVideo` | `video` | Video element controller |
| `playBtn` | `div` | Play/pause icon swap |
| `vcProgress` | `div` | Seek click target |
| `vcFill` | `div` | Progress bar fill width |
| `vcTime` | `div` | Time display text |
| `vcSpeed` | `div` | Speed label text |
| `vcLike` | `div` | Like button state |
| `likeCount` | `span` | Like count display |
| `tabletScrollContainer` | `div` | Scroll animation reference |
| `tabletAnimHeader` | `div` | Header transform target |
| `tabletAnimCard` | `div` | Card 3D transform target |
| `tabletFileName` | `div` | Filename label updater |
| `tpanel-python` | `div` | Python code panel |
| `tpanel-cpp` | `div` | C++ code panel |
| `tpanel-html` | `div` | HTML code panel |
| `tpanel-css` | `div` | CSS code panel |
| `tpanel-js` | `div` | JS code panel |
| `tpanel-git` | `div` | Git code panel |

---

## 20. Assets Necessários

Lista completa de tudo que precisa estar disponível para a página funcionar corretamente:

**Imagens locais (na mesma pasta do `index.html`):**

| Arquivo atual | Sugestão de renome | Onde é referenciado |
|--------------|-------------------|---------------------|
| `WhatsApp Image 2026-03-01 at 23.08.20.jpeg` | `foto-principal.jpg` | `.card-3d-img`, `.story-modal-img img` |
| `WhatsApp Image 2026-03-01 at 10.54.53 copy.jpeg` | `avatar.jpg` | `.card-avatar img` |

**CDNs externas (requerem internet):**

| Recurso | URL base | Crítico? |
|---------|----------|---------|
| Google Fonts (Inter + JetBrains Mono) | `fonts.googleapis.com` | Sim — sem isso as fontes caem para `sans-serif` |
| Devicons (ícones de tecnologia) | `cdn.jsdelivr.net/gh/devicons/devicon` | Não — apenas visual |

**Vídeo (opcional, carregado pelo usuário):**
- Formato aceito: `video/mp4`
- Carregado via `<input type="file">` — não precisa estar no servidor
- Processado localmente via `URL.createObjectURL()`
